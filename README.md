# mundialito
Tabla mundial 2026
members = ['Emi', 'Richi', 'Mido', 'Vivi', 'Jorge', 'Rocio', 'Ricardo']
def calculate_points(prediction_home, prediction_away, actual_home, actual_away):
    points = 0
    # Comprobar si la puntuación es exacta
    if prediction_home == actual_home and prediction_away == actual_away:
        points = 12
    else:
        # Determinar el resultado de la predicción
        pred_outcome = 'win_home' if prediction_home > prediction_away \
                       else ('win_away' if prediction_home < prediction_away else 'draw')

        # Determinar el resultado real
        actual_outcome = 'win_home' if actual_home > actual_away \
                         else ('win_away' if actual_home < actual_away else 'draw')

        # Comprobar si el resultado es correcto
        if pred_outcome == actual_outcome:
            points = 5
    return points
    leaderboard_df = pd.DataFrame({'Member': members, 'Total Points': [0] * len(members)})
leaderboard_df = leaderboard_df.set_index('Member')
match_data = []

def add_match_results(match_name, actual_score_home, actual_score_away, predictions):
    """
    Añade un nuevo resultado de partido y actualiza la tabla de clasificación.

    Args:
        match_name (str): Nombre del partido (por ejemplo, 'Brasil vs Alemania').
        actual_score_home (int): Goles reales del equipo local.
        actual_score_away (int): Goles reales del equipo visitante.
        predictions (dict): Diccionario donde las claves son los nombres de los miembros y los valores son
                            tuplas (pred_home, pred_away) para sus predicciones de puntuación.
    """
    global leaderboard_df, match_data

    match_info = {'Match': match_name, 'Actual Score': f'{actual_score_home}-{actual_score_away}'}

    current_match_points = {}
    for member in members:
        pred_home, pred_away = predictions.get(member, (None, None))
        if pred_home is not None and pred_away is not None:
            points = calculate_points(pred_home, pred_away, actual_score_home, actual_score_away)
            leaderboard_df.loc[member, 'Total Points'] += points
            current_match_points[member] = points
            match_info[f'{member} Prediction'] = f'{pred_home}-{pred_away}'
            match_info[f'{member} Points'] = points
        else:
            current_match_points[member] = 0
            match_info[f'{member} Prediction'] = 'N/A'
            match_info[f'{member} Points'] = 0

    match_data.append(match_info)
    print(f"\n--- Resultados para {match_name} ---")
    for member, points in current_match_points.items():
        print(f"{member}: +{points} puntos")

    print("\nTabla de Clasificación Actualizada:")
    display(leaderboard_df.sort_values(by='Total Points', ascending=False))

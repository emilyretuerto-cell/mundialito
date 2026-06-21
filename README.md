# mundialito
Tabla mundial 2026
leaderboard_df = pd.DataFrame({'Member': members, 'Total Points': [0] * len(members)})
leaderboard_df = leaderboard_df.set_index('Member')
match_data = []

print('Re-running example matches to prepare data for HTML output...')
# Match 1: Argentina vs. Saudi Arabia
match1_predictions = {
    'Emi': (2, 0),
    'Richi': (3, 1),
    'Mido': (2, 0),
    'Vivi': (1, 0),
    'Jorge': (4, 0),
    'Rocio': (2, 1),
    'Ricardo': (3, 0)
}
add_match_results('Argentina vs. Saudi Arabia', actual_score_home=1, actual_score_away=2, predictions=match1_predictions)

# Match 2: Germany vs. Japan
match2_predictions = {
    'Emi': (2, 1),
    'Richi': (1, 1),
    'Mido': (3, 0),
    'Vivi': (2, 0),
    'Jorge': (1, 0),
    'Rocio': (2, 2),
    'Ricardo': (2, 1)
}
add_match_results('Germany vs. Japan', actual_score_home=1, actual_score_away=2, predictions=match2_predictions)

# Match 3: Spain vs. Costa Rica
match3_predictions = {
    'Emi': (3, 0),
    'Richi': (2, 0),
    'Mido': (4, 0),
    'Vivi': (3, 1),
    'Jorge': (2, 0),
    'Rocio': (5, 0),
    'Ricardo': (3, 0)
}
add_match_results('Spain vs. Costa Rica', actual_score_home=7, actual_score_away=0, predictions=match3_predictions)

print('\nData prepared.')

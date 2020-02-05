# Le site web !

Base de données:

player(__id__, username, password, mail, licensed, enabled)
game(__player1_id#, player2_id#, time_started__, winner_id#, server_id#)
server(__id__, name, address, port)
events(__id__, type#, game_id#, time_fired)
event_type(__name__)
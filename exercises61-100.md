61. SELECT Users.username, COUNT(Memberships.user_id)
FROM Users, Groups
LEFT JOIN Memberships ON Users.id = Memberships.user_id AND Groups.id = Memberships.group_id
GROUP BY Users.id;
62. SELECT Groups.name, COUNT(Memberships.group_id)
FROM Users, Groups
LEFT JOIN Memberships ON Users.id = Memberships.user_id AND Groups.id = Memberships.group_id
GROUP BY Groups.id;
63. SELECT Users.username
FROM Users, Groups, Memberships
WHERE Users.id = Memberships.user_id AND Groups.id = Memberships.group_id
GROUP BY Users.id
HAVING COUNT (Memberships.user_id) > 1;
64. 
65.
66. SELECT word FROM Words ORDER BY word COLLATE NOCASE ASC;
67. SELECT name, price FROM Products WHERE price = (SELECT MIN(price) 
FROM Products) ORDER BY name LIMIT 1 OFFSET 0;
68. SELECT name, (SELECT COUNT(*) FROM Products WHERE ABS(A.price -price) <= 1)
FROM Products A;
69.
70. SELECT MIN(ABS(A.price -M.price)) FROM Products A, Products M WHERE A.id <> M.id;
71. SELECT Accounts.owner, COALESCE(SUM(Transactions.change), 0)
FROM Accounts
LEFT JOIN Transactions ON Accounts.id = Transactions.account_id
GROUP BY Accounts.id;
72.
73.
74. SELECT Students.name, COUNT(DISTINCT exercise_id)
FROM Students, Exercises
LEFT JOIN Transmissions ON Students.id = Transmissions.student_id AND Exercises.id = Transmissions.exercise_id AND Transmissions.state = 1
GROUP BY Students.id;
75.
76. SELECT score FROM Results GROUP BY score
ORDER BY COUNT(score) DESC, MIN(score)
LIMIT 1;
77. SELECT score FROM Results ORDER BY score
LIMIT 1 OFFSET ( SELECT (COUNT(id) -1) / 2 FROM Results);
78. SELECT score FROM Results ORDER BY score 
LIMIT 1 OFFSET ( SELECT (COUNT(id) - 1) / 2 FROM Results);
79. SELECT Carts.name, COUNT(Passengers.cart_id)
FROM Carts
LEFT JOIN Passengers ON Carts.id = Passengers.cart_id
GROUP BY Carts.id;
80. SELECT Carts.name, (Carts.seats - COUNT(Passengers.cart_id))
FROM Carts
LEFT JOIN Passengers ON Carts.id = Passengers.cart_id
GROUP BY Carts.id;
81. SELECT ((SELECT SUM(seats) FROM Carts) - (SELECT COUNT(Passengers.cart_id) FROM 
Carts, Passengers WHERE Carts.id = Passengers.cart_id));
82.
83. SELECT Passengers.name
FROM Carts
LEFT JOIN Passengers ON Carts.id = Passengers.cart_id
GROUP BY Carts.id
HAVING COUNT(Passengers.cart_id) = 1;
84. SELECT Carts.name
FROM Carts
LEFT JOIN Passengers ON Carts.id = Passengers.cart_id
GROUP BY Carts.id
HAVING COUNT(Passengers.cart_id) = 0;
85.
86. SELECT Packets.name, COUNT(Contents.packet_id), COUNT(DISTINCT Contents.product_id)
FROM Products, Packets
LEFT JOIN Contents ON Products.id = Contents.product_id AND Packets.id = Contents.packet_id
GROUP BY Packets.id;
87. SELECT Packets.name, Packets.price, COALESCE(SUM(Products.price), 0), 
COALESCE(SUM(Products.price), 0) - Packets.price FROM Packets LEFT JOIN Contents ON Packets.id = Contents.packet_id LEFT JOIN Products ON Products.id = Contents.product_id
GROUP BY Packets.id;
88.
89.
90. SELECT DENSE_RANK() OVER(ORDER BY Results.score DESC, name) AS [rank], name, MAX(score)
FROM Players, Results
WHERE Players.id = Results.player_id
GROUP BY Players.id;
91. SELECT RANK() OVER(ORDER BY Results.score DESC) AS [rank], name, MAX(score)
FROM Players, Results
WHERE Players.id = Results.player_id
GROUP BY Players.id
ORDER BY Results.score DESC, name;
92.
93.
94.
95.
96.
97.
98. SELECT id, ( SELECT COUNT(*) FROM Reservations WHERE NOT 
( v.start > end OR v.end < start) AND id <> v.id ) FROM Reservations v;
99.
100. SELECT MAX(OverlapPerDay) FROM (SELECT COUNT(1) AS OverlapPerDay FROM 
Reservations AS a1, Reservations AS a2
WHERE a1.end BETWEEN a2.start AND a2.end GROUP BY a1.id) AS foo;

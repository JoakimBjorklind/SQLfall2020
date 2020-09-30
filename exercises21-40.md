21. SELECT Players.name, Results.score
FROM Players, Results
WHERE Players.id = Results.player_id;
22. SELECT Players.name, Results.score
FROM Players, Results
WHERE Players.id = Results.player_id AND Players.name = 'Uolevi';
23. SELECT Players.name, Results.score
FROM Players, Results
WHERE Players.id = Results.player_id AND Results.score>250;
24. SELECT Players.name, Results.score
FROM Players, Results
WHERE Players.id = Results.player_id ORDER BY Results.score DESC, name;
25. SELECT Players.name, MAX(Results.score)  
FROM Players, Results
WHERE Players.id = Results.player_id
GROUP BY(Results.player_id);
26. SELECT Players.name, COUNT(Results.player_id)  
FROM Players, Results
WHERE Players.id = Results.player_id
GROUP BY(Results.player_id)
ORDER BY COUNT(Results.player_id) DESC;
27. SELECT Students.name, Courses.name, Gradings.grade
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id;
28. SELECT Courses.name, Gradings.grade
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id AND Students.name ='Uolevi';
29. SELECT Students.name, Gradings.grade
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id AND Courses.name ='Basic Coding';
30. SELECT Students.name, Courses.name, Gradings.grade
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id AND Gradings.grade >=4;
31. SELECT Students.name, COUNT(Gradings.student_id)
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id
GROUP BY Gradings.student_id
ORDER BY Students.id;
32. SELECT Students.name, MAX(Gradings.grade)
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id
GROUP BY Gradings.student_id
ORDER BY Students.name DESC;
33. SELECT Cities.name, Dest.name
FROM Cities, Cities Dest, Flights
WHERE Cities.id = Flights.departure_id AND Dest.id = Flights.destination_id;
34. SELECT Dest.name
FROM Cities, Cities Dest, Flights
WHERE Cities.id = Flights.departure_id AND Dest.id = Flights.destination_id AND Flights.departure_id = 1;
35. SELECT Players.name, COUNT(Results.player_id)  
FROM Players
LEFT JOIN Results ON Players.id = Results.player_id
GROUP BY Players.id;
36.  SELECT Students.name, COUNT(Gradings.grade)
FROM Students, Courses
LEFT JOIN Gradings ON Students.id = Gradings.student_id AND Courses.id = Gradings.course_id
GROUP BY Students.id;
37. SELECT Courses.name, COUNT(Gradings.course_id)
FROM Students, Courses
LEFT JOIN Gradings ON Students.id = Gradings.student_id AND Courses.id = Gradings.course_id
GROUP BY Courses.id;
38. SELECT Courses.name
FROM Students, Courses, Gradings
WHERE Students.id = Gradings.student_id AND Courses.id = Gradings.course_id
GROUP BY Courses.id;
39. SELECT Courses.name
FROM Students, Courses, Gradings
WHERE Courses.id NOT IN (SELECT Gradings.course_id FROM Gradings)
GROUP BY Courses.id;
40. SELECT Cities.name, COUNT(Flights.departure_id)
FROM Cities
LEFT JOIN Flights ON Cities.id = Flights.departure_id
GROUP BY Cities.id 
ORDER BY COUNT(Flights.departure_id) DESC;
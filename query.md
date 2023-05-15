SHOW databases;

USE `university`;

SHOW tables;

1. Selezionare tutti gli studenti nati nel 1990 (160)

DESCRIBE `students`;

SELECT * 

FROM `students`

WHERE `date_of_birth` 

LIKE '1990-%'; <!-- oppure WHERE ('date_of_birth') = 1990; -->

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

DESCRIBE `courses`;

SELECT *

FROM `courses`

WHERE 'cfu' > 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni

DESCRIBE `students`;

SELECT *

FROM `students`

WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

DESCRIBE `courses`;

SELECT *

FROM `courses`

WHERE `period` = 'I semestre'

  AND `year`=1;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

DESCRIBE `exams`;

SELECT *

FROM `exams`

WHERE `date` = '2020-06-20'

  AND `hour`> '14:00:00'; <!-- oppure AND HOUR(`hour`)>= 14 -->

6. Selezionare tutti i corsi di laurea magistrale (38)

DESCRIBE `degrees`;

SELECT *

FROM `degrees`

WHERE `level` = 'magistrale';

7. Da quanti dipartimenti è composta l'università? (12)

DESCRIBE `departments`;

SELECT COUNT(*) AS 'count_departments'

FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

DESCRIBE `teachers`;

SELECT COUNT(*) AS 'nums_teachers_without_phone'

FROM `teachers`

WHERE `phone` IS NULL;
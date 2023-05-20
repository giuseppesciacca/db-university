1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia - (68)

SELECT `s`.*,

       `d`.`name` AS `degree_name`

FROM `students` `s`

INNER JOIN `degrees` `d` ON `s`.`degree_id` = `d`.`id`

WHERE `d`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze (1)

SELECT `degrees`.*,

`departments`.`name` as `department_name`

FROM `degrees`

INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`

WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'

  AND `degrees`.`level` = 'magistrale';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) (11)

SELECT `courses`.*,

       `teachers`.`id` AS `teacher_id`,

       `teachers`.`name` AS `teacher_name`,

       `teachers`.`surname` AS `teacher_surname`

FROM `courses`

JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`

JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`

WHERE `teacher_name` = 'Fulvio'

  AND `teacher_surname` = 'Amato' ;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.*,

       `degrees`.`name` AS `degree_name`,

       `degrees`.`level` AS `degree_level`,

       `departments`.`name` AS `department_name`

FROM `students`

JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`

JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`

ORDER BY `students`.`surname` ASC,

         `students`.`name`

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti (1317)

SELECT `degrees`.*,
       `courses`.`name` AS `course_name`,
       `teachers`.`name` AS `teacher_name`,
       `teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.*,
                `departments`.`name` AS `department_name`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami (32246)

SELECT `student_id`,
       `course_id`,
       COUNT(`course_id`) AS `attempts_for_course`       
FROM `exam_student`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `student_id`,
         `course_id`;

8. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18. (15518)

SELECT `student_id`,
       `course_id`,
       COUNT(`course_id`) AS `attempts_for_course`,
       MIN(`vote`) AS `min_vote`,
       MAX(`vote`) AS `max_vote`
FROM `exam_student` `es`
JOIN `exams` `e` ON `es`.`exam_id` = `e`.`id`
JOIN `courses` `c` ON `e`.`course_id` = `c`.`id`
GROUP BY `student_id`,
         `course_id`
HAVING `min_vote` > 18;
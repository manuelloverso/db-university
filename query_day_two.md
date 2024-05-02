## Group by

- Contare quanti iscritti ci sono stati ogni anno

```sql
 SELECT `enrolment_date` ,COUNT(`id`) AS `NumberOfEnrollments`
 FROM `students`
 GROUP BY `enrolment_date`;
```

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
 SELECT `office_address` ,COUNT(`id`) AS `NumberOfTeachers`
 FROM `teachers`
 GROUP BY `office_address`;
```

- Calcolare la media dei voti di ogni appello d'esame

```sql
 SELECT COUNT(`student_id`) AS `NumberOfStudents` , `exam_id` , ROUND(AVG(`vote`), 1) AS `vote_average`
 FROM `exam_student`
 GROUP BY `exam_id`;
```

- Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
 SELECT COUNT(`id`) AS `numbers_of_degrees` , `department_id`
 FROM `degrees`
 GROUP BY `department_id`;
```

## Joins

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students`.`id` , `students`.`name` , `students`.`surname` , `degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT `degrees`.`id`, `degrees`.`name` , `degrees`.`level` , `departments`.`name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'magistrale';
```

- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT `courses`.`id` , `courses`.`name` , `course_teacher`.`teacher_id`
FROM `courses`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `course_teacher`.`teacher_id` = 44;
```

- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT `students`.`id` , `students`.`name` , `students`.`surname` , `degrees`.`name` AS `degree_name` , `degrees`.`department_id` , `departments`.`name` AS `department_name`
FROM `students`
LEFT JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` , `students`.`name`;
```

- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT `degrees`.`id` , `degrees`.`name` , `courses`.`name` AS `course_name` , `teachers`.`name` AS `teacher_name` , `teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`id`;
```

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT `teachers`.`id` , `teachers`.`name` AS `teacher_name` , `teachers`.`surname` AS `teacher_surname` , `degrees`.`department_id`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE  `degrees`.`department_id` = 5
ORDER BY `teachers`.`id`;
```

- BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql
SELECT `students`.`id` , `students`.`name` , `students`.`surname` , COUNT(`exam_student`.`student_id`) , `courses`.`name` AS `exam_course_name`
FROM `students`
JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
GROUP BY `exam_student`.`student_id` , `exams`.`course_id`;
```

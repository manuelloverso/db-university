## Group by

- Contare quanti iscritti ci sono stati ogni anno
- ```sql
  SELECT `enrolment_date` ,COUNT(id) AS `NumberOfEnrollments`
  FROM `students`
  GROUP BY `enrolment_date`;
  ```

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio
- ```sql
  SELECT `office_address` ,COUNT(id) AS `NumberOfTeachers`
  FROM `teachers`
  GROUP BY `office_address`;
  ```

- Calcolare la media dei voti di ogni appello d'esame
- ```sql
  SELECT COUNT(`student_id`) AS `NumberOfStudents` , `exam_id` , ROUND(AVG(`vote`), 1) AS `vote_average`
  FROM `exam_student`
  GROUP BY `exam_id`;
  ```

- Contare quanti corsi di laurea ci sono per ogni dipartimento

## Joins

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
- BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

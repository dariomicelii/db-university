1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT *
FROM `university`.`students`
WHERE YEAR(`date_of_birth`) = 1990;

```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT *
FROM `university`.`courses`
WHERE `cfu` > 10;

```

3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT *
FROM university.students
WHERE YEAR(CURDATE()) - YEAR(`date_of_birth`) > 30;

```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql
SELECT COUNT(*)
FROM university.courses
WHERE `period` = 'I semestre' AND `year` = 1;

```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT COUNT(*)
FROM university.exams
WHERE `date` = '2020-06-20' AND `hour` > '14:00:00';

```

6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT COUNT(`level`)
FROM university.degrees
WHERE `level` = 'magistrale';

```

7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(`id`)
FROM university.departments;

```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT COUNT(`id`)
FROM university.teachers
WHERE `phone` IS NULL;

```

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

```sql
INSERT INTO `university`.`students` (`degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`) VALUES ('5', 'Dario', 'Miceli', '2001-04-17', 'MCLDRA01D17G702M', '2021-09-15', '839543', 'dariomiceli01@gmail.com');

```

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```sql
UPDATE `university`.`teachers`
SET `office_number` = 126
WHERE `id` = 58;

```

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```sql
DELETE FROM `university`.`students`
WHERE `fiscal_code` = 'MCLDRA01D17G702M';

```

BONUS

1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT
    YEAR(`enrolment_date`)
    COUNT(`id`) AS `enrolled_students`
FROM `students`
GROUP BY YEAR(`enrolment_date`)
ORDER BY(`enrolment_date`)

```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT COUNT(`id`) AS `number_of_teachers`, `office_address`
FROM `university`.`teachers`
GROUP BY `office_address`

```

3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT

```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT COUNT(`id`) `number_of_degrees`, `department_id`
FROM `university`.`degrees`
GROUP BY `department_id`;

```

ESERCIZI JOIN 08/01/2025

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT
	`students`.`id`,
    `students`.`name`,
    `students`.`surname`,
    `degrees`.`name` AS `degree_name`

FROM `university`.`students`

INNER JOIN `university`.`degrees`
ON `students`.`degree_id` = `degrees`.`id`

WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT
	`degrees`.`id`,
    `degrees`.`name`,
    `degrees`.`level`,
    `departments`.`id` AS `department_id`,
    `departments`.`name` AS `department_name`

FROM `university`.`degrees`
INNER JOIN `university`.`departments`
ON `degrees`.`department_id` = `departments`.`id`

WHERE `departments`.`id` = 7 AND `degrees`.`level` = 'magistrale';

```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT *
FROM `university`.`teachers`
INNER JOIN `university`.`courses`
ON `courses`.`id` = `teachers`.`id`

WHERE `teachers`.`id` = 44;

```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT
	`students`.`name` AS `student_name`,
    `students`.`surname` AS `student_surname`,
    `degrees`.`name` AS `degree_name`,
    `departments`.`name` AS `department_name`

FROM `university`.`students`

INNER JOIN `university`.`degrees`
ON `students`.`degree_id` = `degrees`.`id`

INNER JOIN `university`.`departments`
ON `degrees`.`department_id` = `departments`.`id`

ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT
	`degrees`.`id` AS `degree_id`,
	`degrees`.`name` AS `degree_name`,
    `courses`.`id` AS `course_id`,
    `courses`.`name` AS `course_name`,
    `teachers`.`id` AS `teacher_id`,
    `teachers`.`name` AS `teacher_name`,
    `teachers`.`surname` AS `teacher_surname`

FROM `university`.`degrees`
INNER JOIN `university`.`courses`
ON `courses`.`degree_id` = `degrees`.`id`

INNER JOIN `university`.`teachers`
ON `courses`.`id` = `teachers`.`id`;

```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT COUNT(`id`) `number_of_degrees`, `department_id`
FROM `university`.`degrees`
GROUP BY `department_id`;

```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

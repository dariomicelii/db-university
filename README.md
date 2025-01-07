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
WHERE `level` LIKE 'magistrale';

```

7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(*)
FROM university.departments;

```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT COUNT(*)
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
WHERE `id` = '58';

```

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```sql
DELETE FROM `university`.`students`
WHERE `name` LIKE 'Dario' AND `surname` LIKE 'Miceli';

```

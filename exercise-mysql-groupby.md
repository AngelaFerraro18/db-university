# MySQL: GROUP BY

---

### 1. Contare quanti iscritti ci sono stati ogni anno

```
SELECT 
    COUNT(*) AS `number_enrolments`, YEAR(`enrolment_date`) AS `enrolment_year`
FROM
    `students`
GROUP BY `enrolment_year`
ORDER BY `enrolment_year`;

```
### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```

SELECT 
    COUNT(*) AS `teachers_counter`, `office_address` 
FROM
    `teachers`
GROUP BY `office_address`
ORDER BY `office_address`;

```
### 3. Calcolare la media dei voti di ogni appello d'esame

```

SELECT 
    `exam_id`, AVG(`vote`) AS `average_votes`
FROM
    `exam_student`
GROUP BY `exam_id`
ORDER BY `exam_id`;

```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```

SELECT 
    COUNT(*) AS `course_counter`, `department_id`
FROM
    `degrees`
GROUP BY `department_id`
ORDER BY `department_id`;

```
# MySQL: JOIN

---

### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```

SELECT 
    `students`.`id` AS `student_id`,`students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`, `degrees`.`name` AS `degree_name`
FROM
    `students`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'
ORDER BY `student_id`;

```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```

SELECT 
    `degrees`.`id` AS `degrees_id`, `degrees`.`name` AS `degrees_name`, `degrees`.`level` AS `degrees_level`, `departments`. `name` AS `department_name`
FROM
    `departments`
INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`level` = 'magistrale' AND `departments`. `name` = 'Dipartimento di Neuroscienze';

```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT 
    `teachers`.`id` AS `teacher_id`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `courses`.`name` AS `courses_name`
FROM
    `teachers`
INNER JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
INNER JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`name` ='Fulvio' AND `teachers`.`surname` = 'Amato';

```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```

SELECT 
    `students`.`id` AS `student_id`, `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`
FROM
   `students`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` 
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`name`, `students`.`surname`;

```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```
SELECT 
    `degrees`.`id` AS `degrees_id`, `degrees`.`name`  AS `degrees_name`, `courses`.`name` AS `courses_name`, `teachers`.`name` AS `teachers_name`, `teachers`.`surname`  AS `teachers_surname`
FROM
    `degrees`
INNER JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;

```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

*usando GROUP BY:*

```
SELECT
    `teachers`.`id` AS `teachers_id`,`teachers`.`name` AS `teachers_name`, `teachers`.`surname` AS `teachers_surname`, `departments`.`name` AS `department_name`
FROM
    `teachers`
INNER JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
INNER JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
GROUP BY `teachers`.`id`
ORDER BY `teachers`.`id`;

```

*usando DISTINCT:*

```
SELECT DISTINCT
    `teachers`.`id` AS `teachers_id`,`teachers`.`name` AS `teachers_name`, `teachers`.`surname` AS `teachers_surname`, `departments`.`name` AS `department_name`
FROM
    `teachers`
INNER JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
INNER JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teachers`.`id`;

```

### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```

SELECT 
   `students`.`id` AS `student_id`,
   `students`.`name` AS `student_name`,
   `students`.`surname` AS `student_surname`,
   `degrees`.`name`AS `degree_name`,
   `exams`.`id` AS `exam_id`,
   COUNT(`exam_student`.`exam_id`) AS `tries`,
   MAX(`exam_student`.`vote`) AS `max_vote`
FROM `students`
INNER JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id`
INNER JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
GROUP BY `students`.`id`, `exams`.`id`, `degrees`.`name`
HAVING MAX(`exam_student`.`vote`) >= 18
ORDER BY `students`.`name`, `students`.`surname`

```

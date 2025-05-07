# MySQL : query

---

### 1. Selezionare tutti gli studenti nati nel 1990 (160)

SELECT <br> 
    * <br>
FROM <br>
   \`students\` <br>
WHERE YEAR(\`date_of_birth\`) = '1990';

### 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT <br>
    * <br>
FROM <br>
    \`courses\` <br>
WHERE \`cfu\` > '10'; 

### 3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT <br> 
    * <br>
FROM <br>
    \`students\` <br>
WHERE YEAR(CURDATE()) - YEAR(\`date_of_birth\`) > '30';

### 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT <br>
    * <br>
FROM <br>
    \`courses\` <br>
WHERE (\`period\` = 'I semestre') AND (\`year\` = 1); 

### 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT <br>
    * <br>
FROM <br>
    \`exams\` <br>
WHERE (\`date\` = '2020/06/20') AND HOUR(\`hour\`) >=14;

### 6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT <br>
    * <br>
FROM <br>
    \`degrees\` <br>
WHERE \`level\` = 'magistrale';

### 7. Da quanti dipartimenti è composta l'università? (12)

SELECT <br>
    COUNT(\`id\`) AS \`departments_number\` <br>
FROM <br>
    \`departments\`;

### 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT <br>
    COUNT(\`id\`) AS \`teachers_no_phone_number\` <br>
FROM <br>
    \`teachers\` <br>
WHERE \`phone\` IS NULL;
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

    SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` 
    FROM students 
    INNER JOIN degrees 
    ON degrees.id = students.degree_id 
    WHERE degrees.name = 'Corso di Laurea in Economia'; 

2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze

    SELECT `degrees`.`name`, `level`, `departments`.`name` 
    FROM `degrees` 
    INNER JOIN `departments` 
    ON departments.id = degrees.department_id 
    WHERE departments.name = 'Dipartimento di Neuroscienze'; 


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    SELECT `name`, `description`, `course_teacher`.`teacher_id` 
    FROM `courses` 
    LEFT JOIN `course_teacher` 
    ON courses.id = course_teacher.course_id 
    WHERE course_teacher.teacher_id = 44; 

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

    SELECT `students`.`surname`, `students`.`name`, `degrees`.`name`, `departments`.`name` 
    FROM `students` 
    LEFT JOIN degrees ON students.degree_id = degrees.id 
    LEFT JOIN departments on degrees.department_id = departments.id 
    ORDER BY `students`.`surname`, `students`.`name` ASC; 

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

    SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`, `teachers`.`surname` 
    FROM `degrees` 
    LEFT JOIN courses ON courses.degree_id = degrees.id 
    LEFT JOIN course_teacher ON course_teacher.course_id = courses.id 
    LEFT JOIN teachers ON course_teacher.teacher_id = teachers.id; 

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

    SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`, `departments`.`name`, departments.id 
    FROM `teachers` 
    LEFT JOIN `course_teacher` ON course_teacher.teacher_id = teachers.id 
    LEFT JOIN `courses` ON course_teacher.course_id = courses.id 
    LEFT JOIN `degrees` ON degrees.id= courses.degree_id 
    LEFT JOIN departments ON departments.id = degrees.department_id 
    WHERE departments.name = 'Dipartimento di Matematica'


7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

SELECT DISTINCT `courses`.`name`, COUNT(`exam_student`.`vote`) 
AS `tentativi` , `students`.`surname`, `students`.`name` 
FROM `courses` 
JOIN `exams` ON `courses`.`id` = `exams`.`course_id` 
JOIN `exam_student` ON `exams`.`id` = `exam_student`.`exam_id` 
JOIN `students` ON `exam_student`.`student_id` = `students`.`id` 
WHERE `students`.`id` = 1 GROUP BY `courses`.`name`; 
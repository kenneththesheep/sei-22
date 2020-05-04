## Project Post Mortem
Post mortems are important to understand about what happened in a project and actively think about what you learned.

Post-mortems are meant to be a blame-less space open to objective conversation about what went well and what could be improved.

Even in the examples below, where tens of millions of dollars could be lost, the best approach is to think through the series of events that led to the outcome.

Large mistakes are almost never the fault of the developer, but of the sytems and processes in place to prevent errors and problems.

[https://github.com/danluu/post-mortems](https://github.com/danluu/post-mortems)
https://blog.codinghorror.com/the-project-postmortem/



### What to Bring
Please answer the following questions. Take at least 30 minutes to prepare.

#### Approach and Process

1. What in my process and approach to this project would I do differently next time?
<ol>
	<li>Definitely, I have more foresight and put more connection and thoughts to the erd. It was to nearing the result portion that I realise having another id connection helps in easing the process of the result management</li>
	<li>I felt I have taken on a behemoth task which grew from what looks so simple into a major 6 days LOTR major war. Really need to be more wary and think carefully before committing the idea to task.</li>
	<li>I went bashing in, and kinda lost stamina towards the end. Need to really pace myself properly.</li>
</ol>
1. What in my process and approach to this project went well that I would repeat next time?
<ol>
	<li>What really helped is do what I know first. Connect the files and make sure the first output is on the browser.</li>
	<li>Also, I felt the category for the models and controllers were quite well planned and flowed really naturally.</li>
</ol>
--

#### Code and Code Design

1. What in my code and program design in the project would I do differently next time?

<ol>
	<li>I need a more effective way to deal with the creation of pdf</li>

<li>AJAX/DOM gave me hell when it came to the structuring, especially where to place div and form in the correct position. </li>
	<li>I really hope to find a way to be able to store fswrite files to remote server and allow user to download. </li>
	
</ol>

Creation of pdf
   console.log(data.studentname);
    let nameFile = data.studentname.substring(6);
    nameFile = nameFile.replace(/\s/g, '_');
    console.log(nameFile);
var doc = new PDFDocument();
let downloadDirectory = downloadsFolder();
var stream = doc.pipe(fs.createWriteStream(downloadDirectory +'/'+ nameFile +'_individualReport.pdf'));
console.log(data.stuentclass);
console.log(downloadDirectory);
doc
  .text('', 180, 30)
  .font('Times-Roman', 30)
  .fontSize(40)
  .font('Times-Bold', 20)
  .text('HDP Result Slip', {
    width: 500,
    align: 'center',
    indent: 30,
    columns: 2,
    height: 300,
    ellipsis: true
  });
  doc
   .font('Times-Roman', 20)
  .text(data.studentname, 30, 90)
  .font('Times-Roman', 20)
  .moveDown();
 doc
  .text(data.stuentclass, 30, 120)
  .font('Times-Bold', 20);
  console.log("length is "+ data.sa1.length);
if(data.sa1.length===4)
{
doc
    .text("Subject Name", 30, 170)
    .text("SA1", 200, 170)
    .text("SA2", 290, 170)
    .text("Overall", 390, 170)
    .font('Times-Roman', 20)
    .text(data.subjectName[0], 30, 220)
    .text(data.sa1[0], 200, 220)
    .text(data.sa2[0], 290, 220)
    .text(data.overall[0], 390, 220)
    .text(data.subjectName[1], 30, 270)
    .text(data.sa1[1], 200, 270)
    .text(data.sa2[1], 290, 270)
    .text(data.overall[1], 390, 270)
    .text(data.subjectName[2], 30, 320)
    .text(data.sa1[2], 200, 320)
    .text(data.sa2[2], 290, 320)
    .text(data.overall[2], 390, 320)
    .text(data.subjectName[3], 30, 370)
    .text(data.sa1[3], 200, 370)
    .text(data.sa2[3], 290, 370)
    .text(data.overall[3], 390, 370)
    .text(data.overallPercent, 30, 430)
    .text(data.passStatus, 30, 480)
    .text(data.promotionStatus, 270, 480)
    .text(data.conductgrade, 30, 530)
    .text(data.remark, 30, 580)
    .text("V/Principal's", 30, 670)
    .text("signature", 30, 690)
    .text("Teacher's ", 200, 670)
    .text("signature", 200, 690)
    .text("Parent/Guardian's ", 390, 670)
    .text("signature", 390, 690);
} ..........
1. What in my code and program design in the project went well? Is there anything I would do the same next time?
<ol>
	<li>I don't know how but I linked more than 2 tables, especially towards the second half of the assignment. What became tough initially became an essential tool to complete many of the task ahead</li>
	<li>Creating the csv file was awesome.</li>
</ol>

let downloadAllResult = (userlogin, callback) => {
    console.log("%%%%%%%%%%%%%%%%%%%%%%Conduct%%%%%%%%%%%%%%%%%%%%%%%%");
    console.log(userlogin);
    let query = 'SELECT student_class.student_id, students.name, subject.subjectname, result.SA1, result.SA2, result.overall  FROM teachers INNER JOIN teacher_class ON (teachers.id= teacher_class.teacher_id) INNER JOIN student_class ON(teacher_class.class_id = student_class.class_id) INNER JOIN students ON (student_class.student_id = students.id ) INNER JOIN student_subject_result_class ON (student_subject_result_class.student_id = students.id) INNER JOIN result ON ( student_subject_result_class.result_id = result.id) INNER JOIN subject ON ( subject.id= student_subject_result_class.subject_id)  WHERE teacher_id = ($1)';
    //let query = 'SELECT * FROM teachers';
    let loginname = [userlogin.teacher_id];
    //loginname= [ 'bobobobob'];
    let outgoingStatus = {};
    dbPoolInstance.query(query, loginname, (error, queryResult) => {
      if( error ){

        // invoke callback function with results after query has executed
        console.log(error)
        callback(error, null);

      }else{

        // invoke callback function with results after query has executed
        let downloadDirectory = downloadsFolder();
        console.log(downloadsFolder());
        console.log(downloadDirectory);
      const jsonData = JSON.parse(JSON.stringify(queryResult.rows));
      console.log("jsonData", jsonData);

      const json2csvParser = new Json2csvParser({ header: true });
      const csv = json2csvParser.parse(jsonData);

      /*fs.writeFile(downloadDirectory+"/bezkoder_postgresql_fs.csv", csv, function(error)*/
      fs.writeFile("public/csv/class_result.csv", csv, function(error){
        if (error) throw error;
        console.log("class_result.csv successfully!");
        console.log("%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%");
        console.log(downloadsFolder());
      });
            fs.writeFile(downloadDirectory+"/class_result.csv", csv, function(error){
        if (error) throw error;
        console.log("Write to class_result.csv successfully!");
        console.log("%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%");
        console.log(downloadsFolder());
      });

            outgoingStatus = queryResult.rows;
          callback(null, "Write to class_result.csv successfully!");


      }
    });
  };
  For each, please include code examples.
  1. Code snippet up to 20 lines.
  2. Code design documents or architecture drawings / diagrams.

#### WDI Unit 2 Post Mortem
1. What habits did I use during this unit that helped me?
Always start small. Make sure each objective is hit before progressing into a gigantic structure. Always experiment and keep an eye where the data has flown to. 
2. What habits did I have during this unit that I can improve on?
I guess I was pretty distracted. I kinda stop relying on google as much as it brings more confusion than just following the given code from floobits, previous or git book(provided there are no errors.)
3. How is the overall level of the course during this unit? (instruction, course materials, etc.)
To be honest, I was extremely lost because in the midst of the lecture, I was diverted several time(thanks to circuit breaker) and by the time I return, I was like in a daze what happened. I had to really go through step by step from whatever resources I have and navigated my way, especially for complex topics like mvc and ajax. 
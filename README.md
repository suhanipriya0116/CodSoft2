#THIS IS FRONT END CODE
THIS BASICALLY CREATED THE "CREATE QUIZ" PAGE 

<!DOCTYPE html>
<html>

<head>

<title>Create Quiz</title>

<link rel="stylesheet"
href="style.css">

</head>

<body>

<h2>Create Quiz</h2>

<input id="question"
placeholder="Question">

<br><br>

<input id="op1"
placeholder="Option 1">

<br><br>

<input id="op2"
placeholder="Option 2">

<br><br>

<input id="op3"
placeholder="Option 3">

<br><br>

<input id="op4"
placeholder="Option 4">

<br><br>

<input id="answer"
placeholder="Correct Option Number">

<br><br>

<button onclick="saveQuestion()">
Add Question
</button>

<h3>Added Questions</h3>
<div id="questionList"></div>

<script src="create.js"></script>

</body>

</html>





#THIS IS THE JAVASCRIPT OF THE CODE

let questions =
JSON.parse(localStorage.getItem("quiz"))
|| [];

function saveQuestion(){

let q = {

question:
document.getElementById("question").value,

options:[

document.getElementById("op1").value,

document.getElementById("op2").value,

document.getElementById("op3").value,

document.getElementById("op4").value

],

answer:
document.getElementById("answer").value

};

questions.push(q);

localStorage.setItem(
"quiz",
JSON.stringify(questions)
);

alert("Question Added");
displayQuestions();

}
function displayQuestions(){

let questions =
JSON.parse(localStorage.getItem("quiz")) || [];

let list =
document.getElementById("questionList");

list.innerHTML = "";

questions.forEach((q,index)=>{

list.innerHTML += `
<p>
${index+1}. ${q.question}

<button onclick="deleteQuestion(${index})">
Delete
</button>

</p>
`;

});

}
 
displayQuestions();
function deleteQuestion(index){

let questions =
JSON.parse(localStorage.getItem("quiz")) || [];

questions.splice(index,1);

localStorage.setItem(
"quiz",
JSON.stringify(questions)
);

displayQuestions();

}




#THIS PART OF THE CODE WILL HELP US SHOW THE MAIN PAGE OF THE APPLICATION WHICH WILL ASK THE USER TO EITHER TAKE THE QUIZ OR CREATE ONE

<!DOCTYPE html>
<html>

<head>
<title>Online Quiz Maker</title>

<link rel="stylesheet" href="style.css">

</head>

<body>

    <header>
    <h1>Online Quiz Maker</h1>
    <p>Create and Attempt Quizzes</p>
</header>

<h1>Online Quiz Maker</h1>

<button onclick="location.href='create.html'">
Create Quiz
</button>

<button onclick="location.href='quiz.html'">
Take Quiz
</button>

</body>

</html>






#This page allows users to attempt the quiz.
#It displays the quiz questions on the screen and provides a Submit button so users can submit their answers and see their score


<!DOCTYPE html>
<html>

<head>

<title>Take Quiz</title>

<link rel="stylesheet"
href="style.css">

</head>

<body>

<h2>Take Quiz</h2>

<div id="quizBox"></div>

<button onclick="submitQuiz()">
Submit
</button>

<script src="quiz.js"></script>

</body>

</html>





#THIS PART DISPLAYS THE QUIZ QUESTION AS WELL AS CALCULATE THE SCORES


let quiz =
JSON.parse(localStorage.getItem("quiz"));

let box =
document.getElementById("quizBox");

quiz.forEach((q,index)=>{

box.innerHTML +=

`
<p>${q.question}</p>

<input type="radio"
name="${index}"
value="1">

${q.options[0]}

<br>

<input type="radio"
name="${index}"
value="2">

${q.options[1]}

<br>

<input type="radio"
name="${index}"
value="3">

${q.options[2]}

<br>

<input type="radio"
name="${index}"
value="4">

${q.options[3]}

<hr>
`;

});
function submitQuiz(){

let score = 0;

quiz.forEach((q,index)=>{

let selected =
document.querySelector(
`input[name="${index}"]:checked`
);

if(selected){

if(selected.value ==
q.answer){

score++;

}

}

});

localStorage.setItem(
"score",
score
);

window.location =
"result.html";

}





#THIS PART DISPLAYS THE RESULT PAGE


<!DOCTYPE html>
<html>

<head>

<title>Result</title>

<link rel="stylesheet"
href="style.css">

</head>

<body>

<h2>Result</h2>

<p id="result"></p>

<script src="result.js"></script>

</body>

</html>





#THIS PART OF THE CODE IS RESPONSIBLE FOR DISPLAYING THE USER'S SCORE


let score =
localStorage.getItem("score");

document.getElementById(
"result"
).innerHTML =
"Your Score : " + score;





#THIS IS THE STYLING PART OD THE CODE
#WE HAVE WRITTEN THIS FOR THE APPEARANCE OF THE APPLICATION

body{
font-family: Arial;
text-align:center;
background:#f4f4f4;
padding:30px;
}

button{
padding:10px 20px;
margin:10px;
cursor:pointer;
}
header{
    background:#e6e6e6;
    padding:15px;
    margin-bottom:20px;
}


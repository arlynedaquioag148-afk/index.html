<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QuizMaster - Pattao National High School</title>

<script src="https://cdn.tailwindcss.com"></script>

<style>
body {
  background: linear-gradient(180deg, #fffaf7, #ffffff);
  font-family: Arial, sans-serif;
}
</style>
</head>

<body class="p-4">

<div class="max-w-3xl mx-auto bg-white p-6 rounded shadow">

<h1 class="text-2xl font-bold text-center text-red-800 mb-4">
QuizMaster – Pattao National High School
</h1>

<!-- USER INFO -->
<div class="grid gap-3 mb-6">
<input id="teacher" class="border p-2 rounded" placeholder="Teacher's Name">
<input id="subject" class="border p-2 rounded" placeholder="Subject">
<input id="student" class="border p-2 rounded" placeholder="Student Name">
</div>

<hr class="mb-6">

<form id="quizForm" class="space-y-6"></form>

<button onclick="submitQuiz()" class="w-full bg-red-800 text-white p-3 rounded">
Submit Quiz
</button>

<div id="result" class="hidden mt-6 p-4 border rounded text-center"></div>

<footer class="text-center mt-6 text-gray-500 text-sm">
© 2025 Reynaldo P. Usigan, Mylene A. Baquiran, Ara Halelei Daquioag
</footer>

</div>

<script>
const questions = [
{
q: "Which part of the computer stores information even when the power is off?",
options: ["CPU", "RAM", "HDD / SSD", "Monitor"],
answer: 2
},
{
q: "What is the main purpose of the CPU?",
options: ["Display images", "Process instructions", "Print documents", "Store data"],
answer: 1
},
{
q: "Which software is used to browse the internet?",
options: ["Operating System", "Spreadsheet", "Presentation", "Web Browser"],
answer: 3
},
{
q: "Changing font size or bold text in Word is called?",
options: ["Data Entry", "Formatting", "Calculating", "Hyperlinking"],
answer: 1
},
{
q: "Which network covers a large geographical area?",
options: ["LAN", "PAN", "WAN", "SAN"],
answer: 2
},
{
q: "Which protocol is used to send email?",
options: ["IP", "POP", "SMTP", "FTP"],
answer: 2
},
{
q: "Why should you back up files?",
options: ["Speed up PC", "Save money", "Recover lost data", "Better colors"],
answer: 2
},
{
q: "Fake emails asking for passwords are called?",
options: ["Spyware", "Virus", "Trojan", "Phishing"],
answer: 3
},
{
q: "Which OS component manages hardware?",
options: ["UI", "Driver", "Application", "Kernel"],
answer: 3
},
{
q: "What identifies a device on a network?",
options: ["MAC", "URL", "IP Address", "DNS"],
answer: 2
}
];

// LOAD QUESTIONS
const form = document.getElementById("quizForm");

questions.forEach((q, i) => {
let div = document.createElement("div");
div.innerHTML = `
<p class="font-semibold">${i + 1}. ${q.q}</p>
${q.options.map((opt, j) => `
<label class="block ml-4">
<input type="radio" name="q${i}" value="${j}"> ${opt}
</label>
`).join("")}
`;
form.appendChild(div);
});

function submitQuiz() {
let score = 0;

questions.forEach((q, i) => {
let selected = document.querySelector(`input[name="q${i}"]:checked`);
if (selected && parseInt(selected.value) === q.answer) {
score++;
}
});

let percent = (score / questions.length) * 100;

let student = document.getElementById("student").value;
let teacher = document.getElementById("teacher").value;
let subject = document.getElementById("subject").value;

let data = { student, teacher, subject, score, percent };
localStorage.setItem("quizResult", JSON.stringify(data));

document.getElementById("result").innerHTML = `
<h2 class="text-xl font-bold mb-2">Quiz Result</h2>
<p><b>Student:</b> ${student}</p>
<p><b>Teacher:</b> ${teacher}</p>
<p><b>Subject:</b> ${subject}</p>
<p><b>Score:</b> ${score} / ${questions.length}</p>
<p><b>Percentage:</b> ${percent.toFixed(2)}%</p>
`;

document.getElementById("result").classList.remove("hidden");
}
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kids Story Creator</title>

<style>
body{
font-family:Arial,Helvetica,sans-serif;
background:#f4f8ff;
margin:0;
padding:40px;
}

.container{
max-width:900px;
margin:auto;
background:white;
padding:30px;
border-radius:15px;
box-shadow:0 10px 25px rgba(0,0,0,.15);
}

h1{
text-align:center;
color:#4a4a4a;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:15px;
}

label{
display:block;
margin-top:15px;
font-weight:bold;
}

input{
width:100%;
padding:10px;
margin-top:5px;
border-radius:8px;
border:1px solid #ccc;
}

button{
margin-top:30px;
width:100%;
padding:15px;
font-size:18px;
background:#4CAF50;
color:white;
border:none;
border-radius:10px;
cursor:pointer;
}

button:hover{
background:#3e9b43;
}

#story{
margin-top:40px;
background:#fff8dc;
padding:20px;
border-radius:12px;
line-height:1.8;
white-space:pre-wrap;
}
.WigglyGoose {
}
</style>

</head>
<body>

<div class="container">

<h1>📖 Ezra, Penelope, and Monolo's Story Generator</h1>

<div class="grid">

<div>
<label>Silly Name 1</label>
<input id="name1">

<label>Silly Name 2</label>
<input id="name2">

<label>Silly Name 3</label>
<input id="name3">
</div>

<div>
<label>Noun 1</label>
<input id="noun1">

<label>Noun 2</label>
<input id="noun2">

<label>Noun 3</label>
<input id="noun3">

<label>Noun 4</label>
<input id="noun4">
</div>

<div>
<label>Adjective 1</label>
<input id="adj1">

<label>Adjective 2</label>
<input id="adj2">

<label>Adjective 3</label>
<input id="adj3">

<label>Adjective 4</label>
<input id="adj4">
</div>

<div>
<label>Verb 1</label>
<input id="verb1">

<label>Verb 2</label>
<input id="verb2">

<label>Verb 3</label>
<input id="verb3">

<label>Verb 4</label>
<input id="verb4">
</div>

<div>
<label>Location 1</label>
<input id="loc1">

<label>Location 2</label>
<input id="loc2">

<label>Location 3</label>
<input id="loc3">
</div>

</div>

<button onclick="generateStory()">Create Story</button>

<div id="story"></div>

</div>

<script>

async function generateStory(){

const data={
name1:document.getElementById("name1").value,
name2:document.getElementById("name2").value,
name3:document.getElementById("name3").value,

noun1:document.getElementById("noun1").value,
noun2:document.getElementById("noun2").value,
noun3:document.getElementById("noun3").value,
noun4:document.getElementById("noun4").value,

adj1:document.getElementById("adj1").value,
adj2:document.getElementById("adj2").value,
adj3:document.getElementById("adj3").value,
adj4:document.getElementById("adj4").value,

verb1:document.getElementById("verb1").value,
verb2:document.getElementById("verb2").value,
verb3:document.getElementById("verb3").value,
verb4:document.getElementById("verb4").value,

loc1:document.getElementById("loc1").value,
loc2:document.getElementById("loc2").value,
loc3:document.getElementById("loc3").value
};

const prompt=`
Write a children's story between 200 and 350 words for children aged 6-10.

Use every one of these words naturally.

Silly Names:
${data.name1}
${data.name2}
${data.name3}

Nouns:
${data.noun1}
${data.noun2}
${data.noun3}
${data.noun4}

Adjectives:
${data.adj1}
${data.adj2}
${data.adj3}
${data.adj4}

Verbs:
${data.verb1}
${data.verb2}
${data.verb3}
${data.verb4}

Locations:
${data.loc1}
${data.loc2}
${data.loc3}

Requirements:
- Funny
- Positive ending
- Every input used at least once
- 200-350 words
`;

document.getElementById("story").innerHTML=
`<h2>Your Prompt</h2>
<p>This prompt is ready to send to ChatGPT or the OpenAI API:</p>
<pre>${prompt}</pre>`;
const response = await fetch("https://api.openai.com/v1/chat/completions", {
method: "POST",
headers: {
"Content-Type": "application/json",
"Authorization": "Bearer YOUR_OPENAI_API_KEY"
},
body: JSON.stringify({
model: "gpt-4.1",
messages: [
{
role: "user",
content: prompt
}
]
})
});

const result = await response.json();

document.getElementById("story").innerHTML =
result.choices[0].message.content;
}

</script>

</body>
</html>

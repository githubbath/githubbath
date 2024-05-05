div class="monitor">
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title> editor </title>
<style>
  .editor {
    width: 100%;
    height: 400px;
    border: 1px solid #ccc;
    font-family: monospace;
    padding: 10px;
    resize: vertical;
    overflow-y: auto;
  }
</style>
</head>
<body>
<h1>typer</h1>
<textarea class="editor" placeholder="Enter your words here..."></textarea>
<script>
  const editor = document.querySelector('.editor');
  
  editor.addEventListener('input', function() {
    localStorage.setItem('code', editor.value);
  });
  
  const savedCode = localStorage.getItem('code');
  if(savedCode) {
    editor.value = savedCode;
  }
</script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Error System</title>
  <style>
    #error-message {
      display: none;
      border: 1px solid red;
      background-color: #ffbaba;
      color: red;
      padding: 10px;
      margin: 10px 0;
    }
  </style>
  <link>
</head>
<body>
  <h1>Error System</h1>
  
  <div id="error-message"></div>
  
  <textarea id="code-editor"></textarea>
  
  <button onclick="checkCode()">Check Code</button>
  
  <script>
    function checkCode() {
      var code = document.getElementById('code-editor').value;
      
      if (code.includes('error')) {
        document.getElementById('error-message').innerText = 'Error found in code!';
        document.getElementById('error-message').style.display = 'block';
      } else {
        document.getElementById('error-message').style.display = 'none';
      }
    }
  </script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
    <title>Code Detector</title>
</head>
<body>
    <textarea id="code-editor" rows="10" cols="50"></textarea>
    <button onclick="detectCode()">Detect Code</button>
    <div id="code-file"></div>

    <script>
        function detectCode() {
            let code = document.getElementById('code-editor').value;
            let codeFile = document.getElementById('code-file');

            if (code.includes('<html>') && code.includes('<body>') && code.includes('<script>')) {
                codeFile.textContent = 'HTML file detected';
            } else if (code.includes('function') && code.includes('let') && code.includes('document')) {
                codeFile.textContent = 'JavaScript file detected';
            } else if (code.includes('def') && code.includes('class') && code.includes('import')) {
                codeFile.textContent = 'Python file detected';
            } else {
                codeFile.textContent = 'Unknown file type';
            }
        }
    </script>
</body>
</html>
<textarea id="code-editor" rows="10" cols="50"></textarea>
<form id="save-form">
  <input type="text" id="file-name" placeholder="Enter file name">
  <button id="save-btn">Save File</button>
</form>
<script>
// Get the textarea and form elements
const codeEditor = document.getElementById('code-editor');
const saveForm = document.getElementById('save-form');

// Add an event listener to the save button
saveForm.addEventListener('submit', function(event) {
  // Prevent the default form submission
  event.preventDefault();
  
  // Get the file name from the input field
  const fileName = document.getElementById('file-name').value;
  
  // Get the code from the textarea
  const code = codeEditor.value;
  
  // Save the file to the Local Storage
  localStorage.setItem(fileName, code);
  
  // Optional: Show a success message
  alert('File saved successfully!');
});
</script>
<select id="file-select">
  <option value="" disabled selected>Select a file</option>
</select>
<script>
// Get the file select element
const fileSelect = document.getElementById('file-select');

// Populate the file select dropdown with the saved file names
for (let i = 0; i < localStorage.length; i++) {
  const fileName = localStorage.key(i);
  const option = document.createElement('option');
  option.value = fileName;
  option.text = fileName;
  fileSelect.appendChild(option);
}

// Add an event listener to the file select dropdown
fileSelect.addEventListener('change', function() {
  // Get the selected file name
  const selectedFileName = fileSelect.value;
  
  // Get the code from the Local Storage and display it in the code editor
  codeEditor.value = localStorage.getItem(selectedFileName);
});
</script>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Code Compiler</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<div class="container">
<textarea id="code" placeholder="Enter your code here"></textarea>
<button onclick="compileCode()">Compile</button>
<textarea id="output" placeholder="Output will be displayed here" readonly></textarea>
</div>
<script src="script.js"></script>
</body>
</html>
<script>
function compileCode() {
  const code = document.getElementById('code').value;
  fetch('https://api.jdoodle.com/v1/execute', {
      method: 'POST',
      headers: {
          'Content-Type': 'application/json',
      },
      body: JSON.stringify({
          script: code,
          language: 'python3' // Change this to the desired language
      }),
  })
  .then(response => response.json())
  .then(data => {
      document.getElementById('output').value = data.output;
  })
  .catch(error => console('Error:', error));
}
</script>
<css
body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  text-align: center;
}

.container {
  max-width: 600px;
  margin: 100px auto;
  padding: 20px;
}

textarea {
  width: 100%;
  height: 200px;
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
></css>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Code Editor</title>
<style>
    .code-editor {
        width: 100%;
        height: 400px;
        border: 1px solid #ccc;
        padding: 10px;
        font-family: 'Courier New', Courier, monospace;
    }
</style>
</head>
<body>
    <div class="code-editor">
        <textarea id="code" cols="30" rows="10" placeholder="Enter your code here"></textarea>
        <button onclick="runCode()">Run</button>
    </div>
    <script>
        function runCode() {
            var code = document.getElementById('code').value;
            try {
                eval(code);
            } catch (error) {
                console.error(error);
            }
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Code Editor App</title>
<style>
  .editor {
    width: 100%;
    height: 400px;
    border: 1px solid #ccc;
    font-family: monospace;
    padding: 10px;
    resize: vertical;
    overflow-y: auto;
  }
</style>
</head>
<body>
<h1>Code Editor</h1>
<textarea class="editor" placeholder="Enter your code here..."></textarea>
<div id="error-message"></div>
<textarea id="code-editor"></textarea>
<button onclick="checkCode()">Check Code</button>
<select id="file-select">
  <option value="" disabled selected>Select a file</option>
</select>
<form id="save-form">
  <input type="text" id="file-name" placeholder="Enter file name">
  <button id="save-btn">Save File</button>
</form>
<div class="container">
    <textarea id="code" placeholder="Enter your code here"></textarea>
    <button onclick="compileCode()">Compile</button>
    <textarea id="output" placeholder="Output will be displayed here" readonly></textarea>
</div>
<div class="code-editor">
    <textarea id="code" cols="30" rows="10" placeholder="Enter your code here"></textarea>
    <button onclick="runCode()">Run</button>
</div>
</div>

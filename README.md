<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Simple Site</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f5f5f5;
            color: #333;
        }
        header {
            background-color: #0077cc;
            color: white;
            padding: 20px;
            text-align: center;
        }
        nav {
            display: flex;
            justify-content: center;
            gap: 20px;
            background-color: #005fa3;
            padding: 10px 0;
        }
        nav a {
            color: white;
            text-decoration: none;
            font-weight: bold;
        }
        main {
            padding: 50px;
            text-align: center;
        }
        footer {
            background-color: #0077cc;
            color: white;
            text-align: center;
            padding: 10px;
        }
        button {
            background-color: #0077cc;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #005fa3;
        }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to My Simple Site</h1>
    </header>
    <nav>
        <a href="#home">Home</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
    </nav>
    <main>
        <h2>Simple, Clean, Professional</h2>
        <p>This is a free simple website template. You can edit it as you like!</p>
        <button onclick="alert('Hello from your website!')">Click Me</button>
    </main>
    <footer>
        &copy; 2025 My Simple Site
    </footer>
</body>
</html>

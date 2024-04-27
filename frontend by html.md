<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spotify Playlist Generator</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f5f5f5;
        }
        .container {
            text-align: center;
        }
        .btn-primary {
            background-color: #1DB954;
            border-color: #1DB954;
        }
        .btn-primary:hover {
            background-color: #1ED760;
            border-color: #1ED760;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="mb-4">Welcome to the Spotify Playlist Generator!</h1>
        <p>
            <a href="{{ url_for('login') }}" class="btn btn-primary btn-lg">
                <i class="fab fa-spotify mr-2"></i>
                Login with Spotify
            </a>
        </p>
    </div>
    <script src="https://kit.fontawesome.com/your-font-awesome-kit.js" crossorigin="anonymous"></script>
</body>
</html>

# Widget demo version

      <!doctype html>
      <html>
      <head>
        <meta charset=utf-8>
        <meta http-equiv=X-UA-Compatible content="IE=edge">
        <meta name=viewport content="width=device-width,initial-scale=1">
        <!-- widget source css -->
        <link href="./css/app.css" rel=stylesheet>
        <style>
          .container-fluid {
            width: 300px;
            height: 250px;
          }
        </style>
      </head>

      <body>
      <div class="container-fluid">
        <vue-widget
          type="u_type"
          param1="a"
          param2="b"
          token="u_token"
        >
        </vue-widget>
      </div>

      <!-- widget source js -->
      <script src="./js/app.js"></script>
      </body>

      </html>

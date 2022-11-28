# docker_tasks, Проектирование информационных систем
Серверное приложение выполнено на платформе NodeJS:

const express = require("express");
const app = express();

const port = 8080;

let counter = 0;

app.get("/", (_, res) => {
  res.end(JSON.stringify(counter));
});

app.get("/stat", (_, res) => {
  res.end(JSON.stringify(counter++));
});

app.get("/about", (_, res) => {
  const html = `<p>Hi, I'm Marina</p>`;

  res.writeHead(200, { "Content-Type": "text/html" });
  res.end(html);
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});

Файл

FROM node:latest
WORKDIR /app

COPY [".", "."]

RUN ls
RUN npm install


EXPOSE 8080

CMD [ "node", "app.js" ]

Сборка образа, его помещение в Docker Hub и запуск контейнера:

docker build -t maprok/task5

docker push maprok/task5

docker run maprok/task5

FROM node:lts-alpine

LABEL io.k8s.display-name="stats-api" \
      io.k8s.description="stats-api service from the todoapp" \
      io.openshift.expose-services="8080:http"

ENV PORT 8080
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

CMD ["npm", "start"]
# dev stage
FROM node:19-alpine as dev

ENV NODE_ENV development

ARG REACT_APP_BASE_API
ENV REACT_APP_BASE_API $REACT_APP_BASE_API

# setup workdir (next commands will run under this context, but also the running container will inherit this - if not overriden at runtime)
WORKDIR /usr/src/app/

# Build App
# - copy package.json and yarn.lock (optimise image build - copy only these files and run install, if these change rarely we can reuse this image layer too)
COPY package*.json ./

# - install packages (optimise image build - run just install after copying package.json, we hope these will change rarer as the code, so we can reuse this image layer too)
RUN npm i

# - copy the rest of the code (except the ones in .dockerignore) (optimise image build - we expect these to change everytime, so keep this as late as possible)
COPY . .

EXPOSE 8080

CMD ["npm", "start"]

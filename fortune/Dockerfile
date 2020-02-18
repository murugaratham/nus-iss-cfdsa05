# use node latest image as base
FROM node:latest

# environment variables for fortune app
ENV APP_PORT=3000
ENV APP_ROOT=/app

# create $APP_ROOT directory
# cd into $APP_ROOT
WORKDIR ${APP_ROOT}

# Copy application files into $APP_ROOT
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views

# install dependencies using package.json
RUN npm install

# configure healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# what port application is using
EXPOSE ${APP_PORT}

# how to run the program
ENTRYPOINT ["node", "main.js"]
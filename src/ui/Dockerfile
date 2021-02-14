#
# Stage 1: Build Angular app
#

FROM node:lts-alpine AS build
ARG CONFIGURATION=production

WORKDIR /opt/ng

# copy only npm instructions (so that this can be cached if not changed)
COPY package*.json ./

# pull dependencies (so that this can be cached if not changed)
RUN npm install

ENV PATH="./node_modules/.bin:$PATH" 

# copy angular files (will be changing, this image layer is unlikely to be cached)
COPY . ./ 

RUN ng build --output-path ./dist --configuration $CONFIGURATION


#
# Stage 2: Copy to runtime
#

FROM nginx:stable AS runtime

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build /opt/ng/dist /usr/share/nginx/html

EXPOSE 80
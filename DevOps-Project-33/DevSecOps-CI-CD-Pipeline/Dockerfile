#
#    Copyright 2010-2023 the original author or authors.
#
#    Licensed under the Apache License, Version 2.0 (the "License");
#    you may not use this file except in compliance with the License.
#    You may obtain a copy of the License at
#
#       https://www.apache.org/licenses/LICENSE-2.0
#
#    Unless required by applicable law or agreed to in writing, software
#    distributed under the License is distributed on an "AS IS" BASIS,
#    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#    See the License for the specific language governing permissions and
#    limitations under the License.
#
# Use official Maven + JDK image
# Use Maven + JDK 17 image for build

# Stage 1: Build the WAR file
FROM maven:3.9.3-eclipse-temurin-17 AS build

WORKDIR /app
COPY . /app

RUN mvn clean install -DskipTests -Dlicense.skip=true


# Stage 2: Runtime using Tomcat
FROM tomcat:9.0-jdk17-temurin

# Remove default apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy WAR to Tomcat webapps directory
COPY --from=build /app/target/jpetstore.war /usr/local/tomcat/webapps/jpetstore.war

# Expose Tomcat port
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]

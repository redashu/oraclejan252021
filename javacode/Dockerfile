FROM java
MAINTAINER  ashutoshh
RUN mkdir /jcode
COPY hello.java  /jcode/hello.java
WORKDIR  /jcode
RUN javac hello.java 
# compiling java code 
CMD ["java","myclass"] 
# default parent process 
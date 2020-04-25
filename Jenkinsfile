// Licensed to the Apache Software Foundation (ASF) under one or more
// contributor license agreements.  See the NOTICE file distributed with
// this work for additional information regarding copyright ownership.
// The ASF licenses this file to You under the Apache License, Version 2.0
// (the "License"); you may not use this file except in compliance with
// the License.  You may obtain a copy of the License at
//
//    http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.


pipeline {
    agent {
        docker { image 'jdk8-gradle' }
    }
    stages {
            stage('SCM Checkout') {
        	   steps{
        	         checkout scm
        	   }
        	}

        	stage('Gradle Version'){
        	 steps{
        	    sh 'gradle --version'
        	    }
        	}

        	stage('clean') {
        	 steps{
        	    sh 'gradle clean'
        	    }
        	}
        	stage ('compile') {
        	 steps{
        	    sh 'gradle clean compileJava compileScala compileTestJava compileTestScala spotlessScalaCheck checkstyleMain checkstyleTest spotbugsMain rat --profile --no-daemon --continue -PxmlSpotBugsReport=true'
        	    }
        	}

        	stage('Test') {
        	 steps{
        	    sh 'gradle unitTest --profile --no-daemon --continue -PtestLoggingEvents=started,passed,skipped,failed'
        	    }
        	}

        	stage('BuildJar') {
        	 steps{
        	    sh 'gradle jar'
        	    }
        	}
        	stage('BuildSourceJar'){
        	 steps{
        	    sh 'gradle srcJar'
        	    }
        	}
    }
}

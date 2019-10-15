#!/usr/bin/env groovy

import java.net.URL

node{
    stage('Git Checkout'){
        git 'https://github.com/Bindu2301/DevOpsClassCodes.git'
        
    }
    stage('Compile'){
        withMaven(maven:'MyMaven'){
            sh 'mvn compile'
        }
    }
    stage('Review'){
        try{
             withMaven(maven:'MyMaven'){
            sh 'mvn pmd:pmd'
        }
        }finally{
            pmd canComputeNew: 'false', defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''
        }
   }
   stage('Test'){
           try{
                withMaven(maven:'MyMaven'){
                    sh 'mvn test'
           }
       }finally{
           junit 'target/surefire-reports/*.xml'
       }
   }
   stage('CovergareCheck'){
       try{
           withMaven(maven:'MyMaven'){
               sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
           }
       }finally{
            coberturaReportFile: 'target/site/cobertura/coverage.xml'
        }
           
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}

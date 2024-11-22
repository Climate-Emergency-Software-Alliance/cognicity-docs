# About Cognicity 
CogniCity OSS is a free and open source software for community-led disaster response and recovery in highly dense urban environments. Designed, tested, and operationally deployed in Southeast Asia’s monsoon flooding, the system uses a novel humanitarian chatbot model to crowdsource disaster information through social media channels and then gathers, sorts, and displays these solicited reports in real-time on a web-based, mobile-centric map. The system operates as critical urban infrastructure that enables robust, reliable information sharing and communication among residents, government agencies, and first responders.

## Overview
This repository is responsible for giving a detailed information about how to setup a new instance of congincity for your country.

## Tech Stack
Frontend : Auerila Framework , AngularJs

Backend : NodeJS

Infrastructure : AWS , AWS Lambda 

## Data flow
![image](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/assets/39596102/b383636c-0961-427b-baf3-197e34fa83c8)

## Setup
Cognicity follows microservice architecture and so has 3 main repositories i,e Riskmap (Client map , where all the reports are shown) , Cards (Cards for reporting disasters) , cognicity-serverless (Backend of cognicity) to be configured

- [Riskmap](https://github.com/Climate-Emergency-Software-Alliance/riskmap)
- [Cards](https://github.com/Climate-Emergency-Software-Alliance/cognicity-cards-ng)
- [Cognicity-serverless](https://github.com/Climate-Emergency-Software-Alliance/cognicity-serverless)

## Steps Involved to Deploy
Deplyoment Steps can be found [here](https://github.com/Climate-Emergency-Software-Alliance/cognicity-docs/blob/main/docs/deployment.md)

## Current Deployments
- [Petabencana.id](https://petabencana.id/)
- [Mapakalamidad.ph](https://mapakalamidad.ph/)



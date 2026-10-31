# 🏥 Mission Hospital Package Pricing Analysis Using R

This project analyzes hospital costs and explores the factors influencing total hospital expenditure using **R and RStudio**.

### Key Features

* Data cleaning and missing-value treatment
* Categorical variable encoding and dummy-variable creation
* Correlation analysis and exploratory data analysis
* Multiple linear regression modeling
* Multicollinearity analysis using VIF
* Hospital cost prediction and visualization

### Tools & Technologies

**R | RStudio | Tidyverse | Multiple Linear Regression | Statistical Analysis**

**Objective:** To explore relationships between patient characteristics, hospital stay, implant costs, and total hospital costs using statistical modeling.
## Code 
missionML <- read.csv("C:/Users/imrah/Downloads/missionML.csv", stringsAsFactors=TRUE)
summary(missionML)

#Missing Values 
library(tidyverse)
missionML <- missionML %>%
  mutate(across(where(is.numeric),
                ~ ifelse(is.na(.), mean(., na.rm = TRUE), .)))
#label Encoding
missionML$TYPE.OF.ADMSN <- ifelse(missionML$TYPE.OF.ADMSN=="EMERGENCY",1,0)
missionML$IMPLANT.USED..Y.N. <- ifelse(missionML$IMPLANT.USED..Y.N.=="Y",1,0)

#Dummy variables 
library(fastDummies)
missionML = dummy_cols(
  missionML,
  select_columns = c(
    "KEY.COMPLAINTS..CODE",
    "PAST.MEDICAL.HISTORY.CODE",
    "MODE.OF.ARRIVAL"))
  
#correlation
cr = cor(missionML[sapply(missionML,is.numeric)])
cr 
library(corrplot)
corrplot.mixed(cr)

#divide the data set into training and testing 
library(caTools)
set.seed(11)
split=sample.split(missionML$TOTAL.COST.TO.HOSPITAL,SplitRatio = 0.7)
training = subset(missionML,split==TRUE)
testing = subset(missionML,split==FALSE)

library(psych)

#Heteroscedasticity
training$TOTAL.COST.TO.HOSPITAL = log(training$TOTAL.COST.TO.HOSPITAL)
testing$TOTAL.COST.TO.HOSPITAL = log(testing$TOTAL.COST.TO.HOSPITAL)

pairs.panels(training[c("LENGTH.OF.STAY...ICU",
                        "TOTAL.LENGTH.OF.STAY",
                        "LENGTH.OF.STAY..WARD",
                        "COST.OF.IMPLANT",
                        "AGE",
                        "CREATININE",
                        "BP..HIGH",
                        "HR.PULSE",
                        "BODY.WEIGHT",
                        "BMI",
                        "IMPLANT.USED..Y.N.",
                        "TYPE.OF.ADMSN",
                        "KEY.COMPLAINTS..CODE",
                        "PAST.MEDICAL.HISTORY.CODE",
                        "MODE.OF.ARRIVAL","TOTAL.COST.TO.HOSPITAL")])

#Built The Model 
library(car)
model1 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
                        TOTAL.LENGTH.OF.STAY,data = training)
summary(model1)
vif(model1)

model2 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+LENGTH.OF.STAY..WARD
                        ,data = training)
summary(model2)
vif(model2)
model3 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT
            ,data = training)
summary(model3)
vif(model3)

model4 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+AGE
            ,data = training)
summary(model4)
vif(model4)

model5 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+AGE+CREATININE
            ,data = training)
summary(model5)
vif(model5)

model6 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+AGE+BP..HIGH
            ,data = training)
summary(model6)
vif(model6)

model7 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+AGE+BP..HIGH+HR.PULSE
            ,data = training)
summary(model7)
vif(model7)


model8 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+AGE+BP..HIGH+HR.PULSE+BODY.WEIGHT
            ,data = training)
summary(model8)
vif(model8)

model9 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT
            ,data = training)
summary(model9)
vif(model9)

model10 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+BMI
            ,data = training)
summary(model10)
vif(model10)

model11 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
               TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+IMPLANT.USED..Y.N.
             ,data = training)
summary(model11)
vif(model11)

model12 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+TYPE.OF.ADMSN
            ,data = training)
summary(model12)
vif(model12)

model13 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+KEY.COMPLAINTS..CODE
            ,data = training)
summary(model13)
vif(model13)

model14 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+PAST.MEDICAL.HISTORY.CODE
            ,data = training)
summary(model14)
vif(model14)

model15 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+MODE.OF.ARRIVAL
            ,data = training)
summary(model15)
vif(model15)

model16 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+AGE
            ,data = training)
summary(model16)
vif(model16)

model17 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
               TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+BP..HIGH
             ,data = training)
summary(model17)
vif(model17)

model18 = lm(TOTAL.COST.TO.HOSPITAL~TOTAL.LENGTH.OF.STAY+
             COST.OF.IMPLANT+
             AGE+
             CREATININE+
             BP..HIGH+
             HR.PULSE+
             BODY.WEIGHT+
             BMI+
             IMPLANT.USED..Y.N.+
             TYPE.OF.ADMSN+
             KEY.COMPLAINTS..CODE+
             PAST.MEDICAL.HISTORY.CODE+
             MODE.OF.ARRIVAL,data = training)
summary(model18)
vif(model17)

model18 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+CREATININE
            ,data = training)
summary(model18)
vif(model18)

model19 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
               TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+KEY.COMPLAINTS..CODE
             ,data = training)
summary(model19)
vif(model19)

model20 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
               TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+KEY.COMPLAINTS..CODE+
               PAST.MEDICAL.HISTORY.CODE + IMPLANT.USED..Y.N.+AGE,data = training)
summary(model20)
vif(model20)

model21 = lm(TOTAL.COST.TO.HOSPITAL~LENGTH.OF.STAY...ICU+
              TOTAL.LENGTH.OF.STAY+COST.OF.IMPLANT+HR.PULSE+BODY.WEIGHT+AGE
            ,data = training)
summary(model21)
vif(model21)

model22 = lm(TOTAL.COST.TO.HOSPITAL ~ LENGTH.OF.STAY...ICU +AGE+
                   TOTAL.LENGTH.OF.STAY + COST.OF.IMPLANT + HR.PULSE + 
                   BODY.WEIGHT + PAST.MEDICAL.HISTORY.CODE,
                 data = training)
summary(model22)
vif(model22)

model23 = lm(TOTAL.COST.TO.HOSPITAL ~ AGE+LENGTH.OF.STAY..WARD+
               TOTAL.LENGTH.OF.STAY + COST.OF.IMPLANT + HR.PULSE + 
               BODY.WEIGHT + PAST.MEDICAL.HISTORY.CODE,
             data = training)
summary(model23)
vif(model23)


plot(model23$fitted.values,model23$residuals)

#test the model on testing data 
prediction = predict(model23,testing)
head(prediction)

testing$prediction = prediction 
head(testing$TOTAL.COST.TO.HOSPITAL)

plot(testing$TOTAL.COST.TO.HOSPITAL,type="l",col="green")
lines(prediction,type="l",col="blue")



  
  








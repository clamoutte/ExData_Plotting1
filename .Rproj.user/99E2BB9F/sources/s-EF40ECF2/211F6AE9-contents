##This script is for Course Project 1 assignment of 
##Coursera's "Exploratory Data Analysis" course.
#It creates several plots using data from data from the UC Irvine Machine Learning Repository


library(dplyr)
library(lubridate)


##Initialize all variables with hard-coded values
dirName <- "data"
dirPath <- paste0("./",dirName,"/")
fileURL <- "https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip"
destFileName <- "household_power_consumption.zip"

##names of all unzipped files
unzippedFileName <- "household_power_consumption.txt"
unzippedFilePath <- "./data/household_power_consumption.txt"
##check data directory. If it does not exist, create it.
if(!file.exists(dirName)){
  dir.create(dirName)
}

##download zip file automatically. Should not be a manual step.
destFilePath <- paste0(dirPath,destFileName)
download.file(fileURL,destFilePath)

#unzip files into current directory
unzip(destFilePath, exdir="./data")

#####################################################
##  Read data from files
#####################################################
#Load only the data specified in the assignment
message("Loading data...")
powerData <- read.table(unzippedFilePath, sep = ";", header=TRUE, stringsAsFactors = FALSE) 
##%>% filter(Date %in% c("1/2/2007", "2/2/2007"))

powerData <- powerData %>% 
  mutate(Date = as.Date(Date, format="%d/%m/%Y")) %>% 
  mutate (Global_active_power = as.numeric(Global_active_power)) %>%
  mutate (Sub_metering_1 = as.numeric(Sub_metering_1)) %>%
  mutate (Sub_metering_2 = as.numeric(Sub_metering_2)) %>%
  mutate (Sub_metering_3 = as.numeric(Sub_metering_3)) %>%
  mutate (DateTime = as.POSIXct(paste(Date,Time),tz="")) %>%
  filter (Date %in% c(as.Date("2007-02-01"),as.Date("2007-02-02")))
  
##############################################
##Draw histogram of Global Active Pouwer
##############################################
hist(as.numeric(powerData$Global_active_power),ylim = c(0,1200), col = "red", main = "Global Active Power", xlab = "Global Active Power (kilowattts)")

##################
##Copy to PNG
##################
dev.copy(png, file="plot1.png", width=480, height=480)
dev.off()


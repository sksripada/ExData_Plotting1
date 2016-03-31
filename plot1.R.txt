##Read data from the household_power_consumption.txt file downloaded. This file needs to be in the present working directory
filename <- file("household_power_consumption.txt","r")
##Read the data only for Feb 1,2 of 2007 from the file
myPowerData <- read.table(text = grep("^[1,2]/2/2007",readLines(filename),value=TRUE), sep=";", na.strings="?")
colnames(myPowerData)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering_1","Sub_metering_2","Sub_metering_3")

## Create a new column DateTime combining Date and Time
myPowerData$DateTime <- strptime(paste(myPowerData$Date,myPowerData$Time),"%d/%m/%Y %H:%M:%S")

##First Plot
png("plot1.png",width=480,height=480)
hist(myPowerData$Global_active_power, col="red", xlab = "Global Active Power(kilowatts)",main="Global Active Power")
dev.off()
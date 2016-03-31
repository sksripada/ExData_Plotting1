##Read data from the household_power_consumption.txt file downloaded.This file needs to be in the present working directory
filename <- file("household_power_consumption.txt","r")
##Read the data only for Feb 1,2 of 2007 from the file
myPowerData <- read.table(text = grep("^[1,2]/2/2007",readLines(filename),value=TRUE), sep=";", na.strings="?")
colnames(myPowerData)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering_1","Sub_metering_2","Sub_metering_3")

## Create a new column DateTime combining Date and Time
myPowerData$DateTime <- strptime(paste(myPowerData$Date,myPowerData$Time),"%d/%m/%Y %H:%M:%S")

##Fourth Plot
png("plot4.png",width=480,height=480)
par(mfrow=c(2,2), mar=c(4,4,2,1))
##pic 1
with(myPowerData, plot(DateTime,Global_active_power,type="l",ylab="Global Active Power(kilowatts)",xlab=""))
##pic 2
with(myPowerData, plot(DateTime,Voltage,type="l",xlab="datetime"))
##pic 3
with(myPowerData, plot(DateTime,Sub_metering_1,type="l",ylab="Energy Sub metering ",xlab="", col="grey"))
with(myPowerData,points(DateTime,Sub_metering_2,type="l",col="red"))
with(myPowerData,points(DateTime,Sub_metering_3,type="l",col="blue"))
legend("topright",lty=1,col=c("grey","red","blue"),legend=c("Sub_metering_1","Sub_metering_2","Sub_metering_3"))
##pic 4
with(myPowerData, plot(DateTime,Global_reactive_power,type="l",ylab="Global_reactive_power",xlab="datetime"))
dev.off()


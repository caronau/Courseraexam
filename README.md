# Courseraexam
install.packages("RODBC")
library(RODBC)
dsn_driver <- "{IBM DB2 ODBC Driver}"
dsn_database <- "bludb"
dsn_hostname <- "XXXX"
dsn_port <- "31249"
dsn_protocol <- "TCPIP"
dsn_uid <- "XXXXX"
dsn_pwd <- "XXXXX" 
dsn_security <- "ssl"

conn_path <- paste("DRIVER=", dsn_driver,
                   ";DATABASE=", dsn_database,
                   ";HOSTNAME=", dsn_hostname,
                   ";PORT=", dsn_port,
                   ";PROTOCOL=", dsn_protocol,
                   ";UID=", dsn_uid,
                   ";PWD=", dsn_pwd,
                   ";SECURITY=", dsn_security,
                   sep = "")
conn <- odbcDriverConnect(conn_path)


# CROP_DATA:
df1 <- sqlQuery(conn,
                    "CREATE TABLE CROP_DATAnew3 (
                                      CD_ID INTEGER NOT NULL,

              YEAR DATE NOT NULL,

              CROP_TYPE VARCHAR(20) NOT NULL,

              GEO VARCHAR(20) NOT NULL,

              SEEDED_AREA INTEGER NOT NULL,

              HARVESTED_AREA INTEGER NOT NULL,

              PRODUCTION INTEGER NOT NULL,

              AVG_YIELD INTEGER NOT NULL,

              PRIMARY KEY (CD_ID)
                                      )", 
                    errors=FALSE
                    )

    if (df1 == -1){
        cat ("An error has occurred.\n")
        msg <- odbcGetErrMsg(conn)
        print (msg)
    } else {
        cat ("Table was created successfully.\n")
    }


crop_df <- read.csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-RP0203EN-SkillsNetwork/labs/Final%20Project/Annual_Crop_Data.csv')
farm_df <- read.csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-RP0203EN-SkillsNetwork/labs/Final%20Project/Monthly_Farm_Prices.csv')
monthly_df <- read.csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-RP0203EN-SkillsNetwork/labs/Final%20Project/Monthly_FX.csv')
daily_df <- read.csv('https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-RP0203EN-SkillsNetwork/labs/Final%20Project/Daily_FX.csv')

head(crop_df)
head(farm_df)
head(monthly_df)
head(daily_df)

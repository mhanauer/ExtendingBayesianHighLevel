# ExtendingBayesianHighLevel
# Example for Jags-Ymet-XmetSsubj-MrobustHierQuadWt.R 
#------------------------------------------------------------------------------- 
# Optional generic preliminaries:
graphics.off() # This closes all of R's graphics windows.
rm(list=ls())  # Careful! This clears all of R's memory!
#------------------------------------------------------------------------------- 
# Load data file and specity column names of x (predictor) and y (predicted):

# myData = read.csv( file="IncomeFamszState3yr.csv" , comment.char="#")
# xName = "FamilySize" ; yName = "MedianIncome" ; sName="State" ; wName="SampErr"
# fileNameRoot = "IncomeFamszState3yr-Jags-" 

 myData = read.csv( file="HierLinRegressData.csv" )
 xName = "X" ; yName = "Y" ; sName="Subj" ; wName=NULL
 fileNameRoot = "HierLinRegressData-Quad-Jags-" 

# myData = read.csv( file="BugsRatsData.csv" )
# xName = "Day" ; yName = "Weight" ; sName="Subj" ; wName=NULL
# fileNameRoot = "BugsRatsData-Quad-Jags-" 

graphFileType = "eps" 
#------------------------------------------------------------------------------- 
# Load the relevant model into R's working memory:
source("Jags-Ymet-XmetSsubj-MrobustHierQuadWtMatt'sTest.R")
#------------------------------------------------------------------------------- 
# Generate the MCMC chain:
#startTime = proc.time()
mcmcCoda = genMCMC( data=myData , 
                    xName=xName , yName=yName , sName=sName , wName=wName ,
                    numSavedSteps=20000 , thinSteps=15 , saveName=fileNameRoot )
#stopTime = proc.time()
#duration = stopTime - startTime
#show(duration)
# #------------------------------------------------------------------------------- 
# Get summary statistics of chain:
summaryInfo = smryMCMC( mcmcCoda , saveName=fileNameRoot )
show(summaryInfo)
#------------------------------------------------------------------------------- 

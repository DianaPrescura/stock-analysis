# Green stocks Analysis
Performing analysis on Green Stocks data using Visual Basic for Applications (VBA)
## Overview of Project
     The main purpose of the project is to analyze several green energy stocks from different years (2017 and 2018), in order to help Steve determine if his parents should  invest all their money into DAQO New Energy Corporation or if their funds could be diversified. 

## Analysis and Challenges

    '1a) Create a ticker Index
    Dim tickerIndex as Single
    tickerIndex = 0


    '1b) Create three output arrays   
    ReDim tickerVolumes(12) As Long
    ReDim tickerStartingPrices(12) As Single
    ReDim tickerEndingPrices(12) As Single
    
    ''2a) Create a for loop to initialize the tickerVolumes to zero. 
    For i = 0 To 11
        tickerVolumes(i) = 0
        tickerStartingPrices(i) = 0
        tickerEndingPrices(i) = 0
    Next i
        
    ''2b) Loop over all the rows in the spreadsheet. 
    For i = 2 To RowCount
    
        '3a) Increase volume for current ticker
        tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 9).Value
        
        '3b) Check if the current row is the first row with the selected tickerIndex.
        If Cells(i - 1, 2).Value <> tickers(tickerIndex) Then
        tickerStartingPrices(tickerIndex) = Cells(i, 8).Value
            
            
        'End If
        
        '3c) check if the current row is the last row with the selected ticker
         If Cells(i + 1, 2).Value <> tickers(tickerIndex) Then
        tickerEndingPrices(tickerIndex) = Cells(i, 8).Value
            
            

            '3d Increase the tickerIndex. 
            tickerIndex = tickerIndex + 1
            
        'End If
    
    Next i
    
    '4) Loop through your arrays to output the Ticker, Total Daily Volume, and Return.
    For i = 0 To 11
        
        Worksheets("All Stocks Analysis").Activate
        tickerIndex = i
        Cells(i + 4, 1).Value = tickers(tickerIndex)
        Cells(i + 4, 2).Value = tickerVolumes(tickerIndex)
        Cells(i + 4, 3).Value = tickerEndingPrices(tickerIndex) / tickerStartingPrices(tickerIndex) - 1
        
    Next i
    
    'Formatting
    Worksheets("All Stocks Analysis").Activate
    Range("A3:C3").Font.FontStyle = "Bold"
    Range("A3:C3").Borders(xlEdgeBottom).LineStyle = xlContinuous
    Range("B4:B15").NumberFormat = "#,##0"
    Range("C4:C15").NumberFormat = "0.0%"
    Columns("B").AutoFit

    dataRowStart = 4
    dataRowEnd = 15

    For i = dataRowStart To dataRowEnd
        
        If Cells(i, 3) > 0 Then
            
            Cells(i, 3).Interior.Color = vbGreen
            
        Else
         
            Cells(i, 3).Interior.Color = vbRed
            
        End If
        
    Next i
 
    endTime = Timer
    MsgBox "This code ran in " & (endTime - startTime) & " seconds for the year " & (yearValue)

End Sub


## Results

-   We could state that the green stocks we analyzed performed much better in 2017 than in 2018 regarding the yearly return. It was registered one one hand that the two stocks ENPH and RUN stock had positive returns both years. On the other hand we have noticed that the two stocks increased their daily trading volume. 
 -  Also, we could note that almost all stocks in 2017 had a positive return, except the stock ticker "TERP"
 -  The DQ stock that Steve's parents invested in, had a significant loss in 2018.
 -  Regarding refactoring the script, while doing that it  significantly improved the run time 

### Summary


Advantages or Disadvantages of refactoring code? 
    The main purpose of refactoring code is to render the code efficient which will allow it to run faster, be updated or edited in a quicker manner, and can be duplicated or reused with relative ease.  As apposed to it, the big downsize, the refactoring code could get harder to read and implicit it can get time consuming.

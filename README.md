Sub MultiYrStock():

Dim last_row As Long
Dim last_sum_row As Long
Dim ticker As String
Dim opening As Double
Dim closing As Double
Dim yearly_change As Double
Dim percent_change As Double
Dim total_volume As Double
Dim summary_row As Integer
Dim i As Long
Dim increase_ticker As String
Dim decrease_ticker As String
Dim volume_ticker As String
Dim increase As Double
Dim decrease As Double
Dim volume As Double

Cells(1, 9).Value = "Ticker"
Cells(1, 10).Value = "Yearly Change"
Cells(1, 11).Value = "Percent Change"
Cells(1, 12).Value = "Total Stock Volume"
Cells(1, 16).Value = “Ticker”
Cells(1, 17).Value = “Value”
Cells(2, 15).Value = "Greatest % Increase"
Cells(3, 15).Value = "Greatest % Decrease"
Cells(4, 15).Value = "Greatest Total Volume"

summary_row = 2
last_row = Cells(Rows.Count, 1).End(xlUp).Row
total_volume = 0
opening = Cells(2, 3).Value

For i = 2 To last_row
	total_volume = total_volume + Cells(i, 7).Value
    If Cells(i + 1, 1).Value <> Cells(i, 1).Value Then
        ticker = Cells(i, 1).Value
        closing = Cells(i, 6).Value
        yearly_change = closing - opening
    
    	  If opening <> 0 Then
            percent_change = yearly_change / opening
   	    Else
        	percent_change = 0
   	    End If

        Cells(summary_row, 9).Value = ticker
        Cells(summary_row, 10).Value = yearly_change
        Cells(summary_row, 11).Value = percent_change
        Cells(summary_row, 12).Value = total_volume
        
        Cells(summary_row, 11).NumberFormat = "0.00%"
        
        summary_row = summary_row + 1
        ticker = Cells(i + 1, 1).Value
        opening = Cells(i + 1, 3).Value
        total_volume = 0

    End If
    
Next i

last_sum_row = Cells(Rows.Count, 9).End(xlUp).Row
increase = Cells(2, 11)
decrease = Cells(2, 11)
volume = Cells(2, 12)

For i = 2 To last_sum_row
    If Cells(i, 11).Value > increase Then
        increase = Cells(i, 11).Value
        increase_ticker = Cells(i, 9).Value
    ElseIf Cells(i, 11).Value < decrease Then
        decrease = Cells(i, 11).Value
        decrease_ticker = Cells(i, 9).Value
    End If

    If Cells(i, 12).Value > volume Then
        volume = Cells(i, 12).Value
        volume_ticker = Cells(i, 9).Value
    End If

    If Cells(i, 10).Value > 0 Then
        Cells(i, 10).Interior.ColorIndex = 4
    ElseIf Cells(i, 10).Value < 0 Then
        Cells(i, 10).Interior.ColorIndex = 3
        
    End If

Next i

Cells(2, 16).Value = increase_ticker
Cells(2, 17).Value = increase
Cells(3, 16).Value = decrease_ticker
Cells(3, 17).Value = decrease
Cells(4, 16).Value = volume_ticker
Cells(4, 17).Value = volume

Cells(2, 17).NumberFormat = "0.00%"
Cells(3, 17).NumberFormat = "0.00%"
      
End Sub

# Joe's Automotive performs the following routine maintenance services:

Oil change- $26.00
Lube job - $18.00
Radiator flush - $30.00
Transmission flush - $80.00
Inspection - $15.00
Muffer replacement - $100.00
Tire rotation - $20.00

Joe also performs other non routine services and charges for parts and labor ($20 per hour). Create an application that displays the total for a customers visit to Joes . The form should resemble the one shown below only with the modifications listed at the bottom.

Public Class Form1
'Cost Constants
Dim OilChange As Double = 26.0
Dim LubeJob As Double = 18.0
Dim RadiatorFlush As Double = 30.0
Dim TransmissionFlush As Double = 80.0
Dim Inspection As Double = 15.0
Dim ReplaceMuffler As Double = 100.0
Dim TireRotation As Double = 20.0

'Calculate Total
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
Dim ServNLabor As Double = OilLubeCharges() + FlushCharges() + MiscCharges() + GetLabor()
Dim Labor As Double = TextBox2.Text
Dim Parts As Double = GetParts()
Dim Tax As Double = Taxcharges()
Dim Total As Double = TotalCharges()
TextBox1.Text = Parts.ToString("C")
TextBox2.Text = Labor.ToString("C")
TextBox3.Text = ServNLabor.ToString("C")
TextBox4.Text = Parts.ToString("C")
TextBox5.Text = Tax.ToString("C")
TextBox6.Text = Total.ToString("C")
End Sub

'Clear the form
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button2.Click
ClearFees()
ClearFlushes()
ClearMisc()
ClearOilLube()
ClearOther()
End Sub

'Exit the application
Private Sub Button3_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button3.Click
Me.Close()
End Sub

'Calculates the charges for the oil and lube group box
Function OilLubeCharges()
Dim Charges As Double = 0.0
If CheckBox1.Checked = True Then
Charges = Charges + OilChange
End If
If CheckBox2.Checked = True Then
Charges = Charges + LubeJob
End If
Return Charges
End Function

'Calculates the charges for the flushes group box
Function FlushCharges()
Dim Charges As Double = 0.0
If CheckBox3.Checked = True Then
Charges = Charges + RadiatorFlush
End If
If CheckBox4.Checked = True Then
Charges = Charges + TransmissionFlush
End If
Return Charges
End Function

'Calculates the charges for the Misc. group box
Function MiscCharges()
Dim Charges As Double = 0.0
If CheckBox5.Checked = True Then
Charges = Charges + Inspection
End If
If CheckBox6.Checked = True Then
Charges = Charges + ReplaceMuffler
End If
If CheckBox7.Checked = True Then
Charges = Charges + TireRotation
End If
Return Charges
End Function

'Calculates the charges for the parts textbox
Function GetParts()
Dim Charges As Double = 0.0
Try
Charges = Charges + TextBox1.Text
Catch ex As Exception
MessageBox.Show("Please enter valid input in Parts")
End Try
If Charges <= 0 Then
Charges = 0.0
End If
Return Charges
End Function

'Calculates the charges for the labor textbox
Function GetLabor()
Dim Charges As Double = 0.0
If TextBox2.Text = "" Then
Return Charges
End If
Try
Charges = Charges + TextBox2.Text
Catch ex As Exception
MessageBox.Show("Please enter valid input in Labor")
End Try
If Charges < 0 Then
MessageBox.Show("Please do not enter negative values")
Charges = 0.0
End If
Return Charges
End Function

'Calculates the charges for labor and parts combined
Function OtherCharges()
Dim Charges As Double = 0.0
Charges = GetLabor() + GetParts()
Return Charges
End Function

'Calculates Tax
Function Taxcharges()
Dim Tax As Double = 0.0
If TextBox1.Text = "" Then
Return Tax
End If
Tax = (GetParts() * 0.06)
Return Tax
End Function

'Calculates all charges together
Function TotalCharges()
Dim Charges As Double = 0.0
Charges = OilLubeCharges() + FlushCharges() + MiscCharges() + OtherCharges() + Taxcharges()
Return Charges
End Function

'Clears Group Box 1
Sub ClearOilLube()
CheckBox1.Checked = False
CheckBox2.Checked = False
End Sub

'Clears Group Box 2
Sub ClearFlushes()
CheckBox3.Checked = False
CheckBox4.Checked = False
End Sub

'Clears Group Box 3
Sub ClearMisc()
CheckBox5.Checked = False
CheckBox6.Checked = False
CheckBox7.Checked = False
End Sub

'Clears the parts and labor text boxes
Sub ClearOther()
TextBox1.Text = "$0.00"
TextBox2.Text = "$0.00"
End Sub

'Clears the summary text boxes
Sub ClearFees()
TextBox3.Text = "$0.00"
TextBox4.Text = "$0.00"
TextBox5.Text = "$0.00"
TextBox6.Text = "$0.00"
End Sub
End Class

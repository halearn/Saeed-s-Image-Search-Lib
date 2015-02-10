# Saeed-s-Image-Search-Lib
This Dll Allows You To Scan For A Part Of An Image In The Bigger Image And Get The Position 
 For example you can make an application the clicks on a button on screen 
 
 Sample Use Of The Lib (vb.net):
 You need to import the dll after importing it to the project
 
 Imports BitmapDetector2.Search_Image
 
 Declare Function apimouse_event Lib "user32.dll" Alias "mouse_event" (ByVal dwFlags As Int32, ByVal dX As Int32, ByVal dY As Int32, ByVal cButtons As Int32, ByVal dwExtraInfo As Int32) As Boolean
    Public Const MOUSEEVENTF_LEFTDOWN = &H2
    Public Const MOUSEEVENTF_LEFTUP = &H4
    Private Const MOUSEEVENTF_RIGHTDOWN = &H8
    Private Const MOUSEEVENTF_RIGHTUP = &H10
    
 Private Function PressButton(ByRef image As Bitmap, ByRef press As Boolean, ByRef x As Integer, ByRef y As Integer)
        Dim bounds As Rectangle
        Dim point As New Point
        Dim screenshot As System.Drawing.Bitmap
        Dim graph As Graphics
        bounds = Screen.PrimaryScreen.Bounds
        screenshot = New System.Drawing.Bitmap(bounds.Width, bounds.Height, System.Drawing.Imaging.PixelFormat.Format32bppRgb)
        graph = Graphics.FromImage(screenshot)
        graph.CopyFromScreen(0, 0, 0, 0, bounds.Size, CopyPixelOperation.SourceCopy)
        Dim returnString As Point = BitmapDetector2.Search_Image.search(screenshot, image, 0)
      
        If returnString.X = 0 And returnString.Y = 0 Then
            Return False
        Else
            If press = True Then

                point.X = returnString.X + x
                point.Y = returnString.Y + y
                Windows.Forms.Cursor.Position = point
                Call apimouse_event(MOUSEEVENTF_LEFTDOWN, 0, 0, 0, 0)
                Call apimouse_event(MOUSEEVENTF_LEFTUP, 0, 0, 0, 0)
            Else
                point.X = returnString.X + x
                point.Y = returnString.Y + y
                Windows.Forms.Cursor.Position = point

            End If


            Return True
        End If

    End Function
    ...
    All Copyright Reserved Saeed Suleiman 2015
 
 

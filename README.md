# copy_windows_console_as_html

A methodology for the best possible copying of the windows console to an html file.

## Copying the windows console to an html file.

The purpose of this project is to develop a methodology for the best possible copying of the windows console to an html file. In order to achieve this, two small executable files that run in the windows console are used, namely ConSave.exe and cp_to_utf-8.exe.

An optional prerequisite is the installation of python 3, for easier creation of the mapping file of the active code page to utf-8, using the executable file cp_to_utf-8.exe.

The executable file cp_to_utf-8.exe is a script written in python (specifically it has been written in python 3.10 - 64 bit) and is used to create a mapping file from the active code page of the windows console to utf-8. The procedure is as follows.

* From Start -> Windows System -> Command Prompt open the console and type "chcp". In my case the output is:\
Active code page: 737

* On the website https://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/PC/ select the link corresponding to your active code page and download this webpage as a text file, for example CP437.TXT. Then edit this file with notepad and remove the first few lines, leaving the rest of the lines, that is, from the one that starts with "0x00 0x0000 #NULL" and below. Save this file, for the said example, as cp437_mod.txt.

* Type, for the aforementioned example, "cp_to_utf-8 cp437 cp437_mod.txt test.txt". The first argument, cp437, is the name of the active codepage so change it to your own. The second argument, cp437_mod.txt, is the one we already mentioned before, and the third, test.txt, is an output text file. Open the test.txt file with notepad to see if the mapping is correct. For example, in my case, for active codepage 737 the first three lines appear as follows,\
0xFFFFFF80 0xCE91\
0xFFFFFF81 0xCE92\
0xFFFFFF82 0xCE93\
\. \. \.\
The first column will be the same as yours. As you would notice, the mapping is done in the second half of the original mapping file which for our example is cp437_mod.txt, because the first half is the same in all codepages. Also the hexadecimal number 0xFFFFFF00 has been added with all the hexadecimal elements of the first column (four bytes per character).

* Once you have verified that the mapping in the test.txt file is correct, rename it to CPtoUTF8 (without extension) and copy it to your own profile folder, which is located in the folder "C:\Users".

The executable file ConSave.exe creates an html file using the CPtoUTF8 file. Black is the default background color. In the generated html page, the colors of the console characters are preserved, as shown in the following screenshot.

![Screenshot of a generated html file.](https://github.com/kpatrinos/copy_windows_console_as_html/blob/5631ecec972ad70532837f195426e57e1f5998c7/copy_windows_console_as_html.png)

The consave command is typed in the console that we want to copy. For example:\
``` consave ```\
to create an html file named 'con_text_' + 'datetime'.html in the present working directory, or\
``` consave filename ```\
if you want to give your own filename instead of the default.\
The ```-h``` option is for help.



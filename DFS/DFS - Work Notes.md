
**Distributed File System** (نظام الملفات الموزّع).

طبعا first thing i did is installing DFS roal and this is the pictur pelwo ![[DFS_Instal.JPG]]

and there ar tow roles DFS Namespaces and Dfs Replication i google it and this is the defrinss betwent these tow roles 
so Namespaces is the on rsponsible for sharing files and floders or what ever on the network with one path on over of many domains
but  Replication is about making shur there is bakup and is abuot security and fasting

next


نفتح DFS Mangment من خلال tools 
اول شي بنطبيق ونبفهم مفهوم DFS namespace
تمام نعمل new namespace وبعدين نضيف اسم السيرفر وبعده نعمل اسم لمساحة العمل وانا سميتها Data وهذه الي بتظهر للمستخديمن يعني اذا قرروا انهم يدخلو على الشبكات والمجلدات الي فيها بتكون كذا \\bank.lab\Data\ اسم المجلدات الخاصه بهم على العموم هذا بيكون مساحة العمل الجديدة هم الان ما يعرفون في اي سيرفر موجوده هذه المجلدات لكن ما يمهم الان ان يحصلون عليها عبر خدمة DFS namespace 
وهذه الصورة توضح 
اهم نوعين Namcespace 
![[Namespace_Type.JPG]]

domain-based-namespace 1
stand-alone-namespace     2 
وطبعا ما يمهنا هو رقم 1 الي من خلاله بيتم عمل وتطبيق DFS بالشكل المطلوب

وهذه صورة DFS Console
![[DFS_Console.PNG]]


طبعا دخلت على namespcse 

وهنا قمت باضافة مجلد على dfs consle وقمت بتسميته HR واخترت الهدف الي من بيجيب البيانات المطلوبه منه  مثل ما هو موضح في الصورة Perview og namespace : \\bank.lab\Data\HR  
Foldr tagets: \\DC01\Shares\HR


![[new_folder_HR_zoom.png]]


الان بروح على windows 7 وبدخل على مجلد hr من  خلال الرابط الجديد مثل ما هو موضح  في الصورة

![[HR_User_Folder.PNG]]



خلاص كذا انتهينا من DFS namespace 

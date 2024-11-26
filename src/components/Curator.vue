<script>
import lcc from '@/assets/img/introduction/2007LCC.jpg'
import curatorImg from '@/assets/img/introduction/curator.jpg';
import thirdCurator from '@/assets/img/introduction/thirdCurator.jpg';
import secondCurator from '@/assets/img/introduction/secondCurator.png';
import firstCurator from '@/assets/img/introduction/firstCurator.jpg';

export default {
    data() {
        return {
            count: 1,
            contentData: [
                {
                    title: '紀念館介紹',
                    subTitle: '',
                    img: lcc,
                    content: [
                        {
                            title: '',
                            text: '　　「林之助畫室（林之助紀念館）」原為國立臺中教育大學教職員宿舍，亦為林之助教授故居，建於昭和3（1928）年，採木造雨淋板構造，為日治時期木造雙併宿舍典型建築。建築物由東側之林之助畫室及西側建築所構成，現況西側建築基本上仍維持日治時期宿舍（官舍）之格局與特色，即大正6（1917）年頒布「判任官官舍標準改正」之判任官乙種雙併官舍；東側林之助畫室因林之助教授之使用，在空間上有所變更，呈現特有風格。畫室暨西側建築之建築面積（單棟）約為20坪左右，其空間規模為玄關2疊、座敷8疊、次之間6疊、茶之間6疊，並設有炊事場、踏込、浴廁及便所等。'
                        },
                        {
                            title: '沿革',
                            text: '　　畫室第一次擴建時間應在民國46（1957）年間或之前，林之助教授為了作畫需求，於建築東側擴建畫室。畫室空間在後期曾進行改建，推測應為配合住宅整體之擴建所進行之翻修，改建時間推測應該在民國67（1978）年之前，成為今日林之助畫室（紀念館）之主要樣貌，而該次改建亦為林之助教授親自設計，透過長期配合之工匠進行裝修 。'
                        },
                        {
                            title: '',
                            text: '　　民國95（2006）年，面臨教育部來文須拆除收回老舊宿舍，當時本校楊思偉校長及莊明中主任秘書為表彰林之助教授對膠彩畫的重要貢献和代表意義，決定將宿舍推動保留為文化資產。民國96（2007）年經臺中市文化局審議委會決議，宿舍登錄為歷史建築，102（2013）年本校獲臺中市文化局補助350萬元、林之助家屬捐贈900萬元，以及裕元教育基金會捐贈1000萬元，將宿舍進行修復再利用計畫整建，前後共耗資2,140餘萬元修繕完成。民國104（2015）年6月6日，正式以「林之助紀念館」對外開放免費參觀，現由館方自籌經費管理營運。'
                        },
                        {
                            title: '',
                            text: '　　紀念館藉由舊空間的修復再利用，常態性展出林之助教授複製畫作、膠彩顏料及書信等相關文物；和室展廳則規劃為小型座談及展演空間，平日並播放展示林之助教授專訪介紹影片。為了讓藝術走入民眾生活，本館提供免費預約導覽服務，也持續策畫各項藝文展演活動，透過藝術活動的參與及資源交流，增加民眾的認同。希望民眾在欣賞畫作之餘，也能藉此洞察其細膩的創作思維，延伸體現林之助的生活哲學，進而推動林之助「藝術生活化」、「美術大眾化」的美育理念，推廣膠彩之美。'
                        },
                        {
                            title: '歷程',
                            text: '1928年（昭和3年）     臺中師範學校（今國立臺中教育大學）附屬教師宿舍之興建年代\n 1946年（民國35年）   林之助於臺中師範學校任教並遷入宿舍居住\n 1979年（民國68年）   林之助於臺中師範學校退休\n 2006年（民國95年）   學校將宿舍統一收回，林之助遷出宿舍後移居美國\n 2007年（民國96年）   宿舍以「林之助畫室」之名，由臺中市政府文化局登錄為歷史建築 (府授文資字第0960150246號)\n 2008年（民國97年）   林之助於美國洛杉磯辭世\n 2013年（民國102年）  國立臺中教育大學進行修復再利用計畫\n 2015年（民國104年）  宿舍修繕落成，「林之助畫室（林之助紀念館）」免費開放參觀，由館方自籌經費管理營運\n 2020年（民國109年）  「林之助畫室（林之助紀念館）」變更登錄為紀念建築 (府授文資古字第1090015342號)\n 2021年（民國110年）   林之助夫人 林王彩珠女士於美國洛杉磯辭世\n'
                        },
                    ],
                }, {
                    title: '現任館長',
                    subTitle: '顏名宏 館長',
                    img: curatorImg,
                    content: [
                        {
                            title: '學歷',
                            text: '德國國立紐倫堡造型藝術學院藝術與開放空間系所最高文憑畢業\n AdBK, Akademie der Bildenden Künste Nürnberg, Kunst und öffentlichem Raum(Art and Public Space) , Meisterschüler, （同博士）Germany.'
                        },
                        {
                            title: '現職',
                            text: '■ 國立臺中教育大學文化創意產業設計與營運學系 教授\n ■ 105-114年度「教育部補助高級中等以下學校校園美感環境再造－規劃輔導團隊計畫」計畫主持人'
                        },
                        {
                            title: '曾任',
                            text: '■ 教育部「整合型視覺形式美感教育實驗計畫子計畫：辦理中區美感教育大學基地計畫」計畫主持人2013-2016 \n ■ 文化部第二屆「世界遺產推動委員會」委員 2012-2013 \n ■ 行政院文化建設委員會「社區總體營造推動委員會」委員 1999-2010 \n ■ 教育部「第五、六屆藝術教育推動會」委員 2017-2021'
                        },
                        {
                            title: '專長',
                            text: '　　區域文化研究、文化色彩學、空間符號學、文化人類學、藝術與公共場域理論研究、複合媒體與空間行為展演、藝術與開放空間規劃研究、博物館展示空間策略研究策展、開放空間藝術創作、空間互動裝置藝術創作、數位多媒體互動裝置。'
                        },
                        {
                            title: '重要經歷摘要',
                            text: '2007-2026  曾擔任行政院文化建設委員會、文化部、交通部、教育部、臺北市、新北市、苗栗縣、臺中市、臺南市、高雄市、彰化縣、雲林縣、嘉義縣、花蓮縣等公共藝術審議會委員 \n 2024-2027  文化部第十二屆「財團法人臺灣生活美學基金會」董事 \n 2024、2020、2014「南瀛獎」評審委員 \n 2024、2018、2016、2015、2012「臺灣美術新貌獎」評審委員 \n 2023 「翻浪經緯線-文化工藝的美學實踐展覽策畫執行計畫」策展人 \n 2023-2024  文化部「公共藝術代辦制度諮詢座談及分析藝文採購案」共同主持人 \n 2022-2024 「臺中市第二屆纖維工藝博物館諮詢委員會」委員 \n 2022  文化部「111年全國美術展」評審委員 \n 2022-2024 「臺中市第四、五屆纖維創作獎」評審委員 \n 020 「109學年度全國學生美術比賽」臺中市初賽評審委員 \n 2017-2023  文化部第十、十一屆「財團法人臺灣美術基金會」董事 \n 2019  教育部「2019校園環境美感藝術季」暨「校園美感環境執行研討工作坊」計畫主持人 \n 2019-2021 「嘉義市第七屆有形文化資產審議委員會」委員 \n 2019-2020 「嘉義市第七屆古物審議會」委員 \n 2018  教育部「2018年教育部校園美感環境教育國際案例文件展」策展人 \n 2018  教育部「國際校園美感環境教育論壇」計畫主持人 \n 2016  國防部「國家軍事博物館」諮詢委員 \n 2016  臺北市立美術館「第三屆X-site計畫」 評選委員 \n 2015 「臺中市社區總體營造推動委員會」委員 \n 2012  行政院客家委員會客家文創意商品實品通路 評選委員 \n 2012、2023 「臺中市第十七、二十八屆大墩美展」評審委員 \n 2006  行政院文化建設委員會「區域型文化資產保存與活化再利用」審議委員 \n 2005 「臺中縣第八屆編織工藝獎」評審委員 \n 2005 「臺中縣國際藝術村設置計畫」評審委員 \n 2004 「臺灣省第五十八屆全省美術展覽會」評審委員 \n 2004 「臺中市大墩美展」評審委員 \n 2003-2007 「臺中縣藝術之家」評審委員 \n 2003-2004 「彰化縣磺溪美展」評審委員 \n 2003 「臺灣省第五十七屆全省美術展覽會」評審委員'
                        },
                        {
                            title: '獲獎',
                            text: '2023  國際景觀建築師聯合會(IFLA)「2023亞洲-太平洋洛杉磯景觀設計大獎」(ASIA-PAC LA Awards 2023)之文化和都市景觀類大會榮譽獎 \n 2022  文化部文化資產局「文化部文化資產園區入口意象設置計畫」首獎 \n 2018  中華民國景觀學會「第六屆臺灣景觀大賞」優質獎 \n 2018 「文化部第六屆公共藝術獎」民眾參與獎 \n 2017 「文化部第五屆公共藝術獎」卓越獎 \n 2012 「行政院文化建設委員會第三屆公共藝術獎」最佳教育推廣獎 \n 2009 「行政院文化建設委員會第二屆公共藝術獎」卓越獎 \n 2009 「行政院文化建設委員會第二屆公共藝術獎」最佳策劃獎 \n 1996　德國IHK基金會伏盧森堡二次大戰納粹集中營公開競圖，傑出獎（Wettbewerb fuer ein  Dietrich Bonhoeffer-Zeichen und Gesamtkonzept fuer das ehemalige Konzentrationslager Flossenbuerg Germany） \n 1994  德國國立紐倫堡造型藝術學院年度首獎 \n 1994  德國巴伐利亞銀行(Bayerische Landesbank)開放空間藝術競圖首獎 \n 1993 「臺灣全省美術展覽會」獲永久免審查藝術家資格 \n 1993 「第四十七屆臺灣全省美術展覽會」大會獎 \n 1992 「第四十六屆臺灣全省美術展覽會」教育廳獎 \n 1991 「第四十五屆臺灣全省美術展覽會」教育廳獎 \n 1990 「臺北市第十七屆美展」首獎'
                        },
                    ],
                }, {
                    title: '歷任館長－高永隆',
                    subTitle: '第三任館長\n 任期：111.08.01~113.07.31',
                    img: thirdCurator,
                    content: [
                        {
                            title: '學歷',
                            text: '國立臺灣師範大學藝術學博士\n 國立臺灣師範大學美術研究所碩士\n 國立臺灣師範大學美術系'
                        },
                        {
                            title: '經歷',
                            text: '2022  國立臺中教育大學美術學系教授兼林之助紀念館館長\n 2010  中國美術學院學岩彩畫研究所客座教授\n 2010  中國美術學院學岩彩畫學術委員會委員\n 2009  中國美術學院學岩彩畫創作班講座教授\n 2008  中國人民大學藝術學院岩彩畫專業碩士班講座教授\n 2007  國立臺中教育大學美術系專任助理教授\n 2007  中國文化部重彩岩彩高級研究班客座教授\n 2005  大葉大學造形藝術系專任助理教授 東海大學美術研究所兼任助理教授\n 2004-2005  明道管理學院時尚造形系專任助理教授\n 2003-2004  玄奘人文社會學院視傳系兼任助理教授\n 1999  北京天雅中國重彩画研究所客座教授\n 1997-1998  法國巴黎國際藝術村（Cite Internationale des art,Paris） 駐村藝術家\n 1996-1997  國立臺灣師範大學美術系助理研究員'
                        },
                        {
                            title: '學術專長',
                            text: '膠彩創作、水墨畫創作、藝術理論'
                        },
                        {
                            title: '獲獎／榮譽',
                            text: '2004  中國第三屆岩彩畫大展金獎2004  中國第三屆岩彩畫大展金獎\n 1997  教育部甄選公費赴法國巴黎國際藝術村（Cite Internationale des art）創作研究\n 1987  第42屆全省美展國畫部第二名\n 1986  第41屆全省美展國畫部優選\n 1985  第4屆高雄市美展國畫部第一名\n 1985  第40屆全省美展國畫部第二名\n 1984  第39屆全省美展國畫部第一名\n 1983  第34屆師大美展國畫第一名\n 1997  教育部甄選公費赴法國巴黎國際藝術村（Cite Internationale des art）創作研究\n 1987  第42屆全省美展國畫部第二名\n 1986  第41屆全省美展國畫部優選\n 1985  第4屆高雄市美展國畫部第一名\n 1985  第40屆全省美展國畫部第二名\n 1984  第39屆全省美展國畫部第一名\n 1983  第34屆師大美展國畫第一名'
                        },
                    ],
                }, {
                    title: '歷任館長－侯禎塘',
                    subTitle: '第二任館長\n 任期：110.08.01~111.07.31',
                    img: secondCurator,
                    content: [
                        {
                            title: '學歷',
                            text: '國家考試\n 73年高考及格(司法行政觀護人類科)'
                        },
                        {
                            title: '行政經歷',
                            text: '國立臺中教育大學 副校長\n 國立臺中教育大學 林之助紀念館館長\n 國立臺中教育大學 總務長\n 國立臺中教育大學 教師專業碩士學位學程主任\n 國立臺中教育大學 特殊教育學系主任\n 國立臺中教育大學 特殊教育中心主任\n 台北市教師研習中心 研究員兼研究組組長\n 台北市教師研習中心 教務組組長\n 台南地方法院檢察署 觀護人\n 屏東地方法院檢察署 觀護人\n 台中市沙鹿區北勢國小教師'
                        },
                        {
                            title: '專案/著作/發表',
                            text: '　　國科會專題研究及教育部計畫案主持及共同主持70多件。從事藝術治療、特殊教育師資培育、特殊教育課程教學與輔導之相關研究論述，於期刊發表、研討會主題演講和論文發表計約150多篇。出版學術著作：藝術治療理念與實務、身心障礙教材教法(主編)、特殊教育導論(合著)和資優教育導論(合著)等書。參與國內外美術展覽：雙人展與書畫藝術聯展等計約40餘次。'
                        },
                        {
                            title: '榮譽',
                            text: '臺灣藝術治療學會理事長\n 臺灣師範大學教育學院百大亮點校友(學術類)\n 彰化師範大學傑出校友\n 臺中教育大學傑出校友\n 臺中市北勢國小傑出校友'
                        },
                    ],
                }, {
                    title: '歷任館長－黃位政',
                    subTitle: '首任館長\n 任期：104.08.01~111.01.31',
                    img: firstCurator,
                    content: [
                        {
                            title: '學歷',
                            text: '法國國立巴黎高等美術學院 ENSBA ( ECOLE NATIONALE SUPERIEURE DE BEAUX-ARTS)'
                        },
                        {
                            title: '經歷',
                            text: '獲聘林之助紀念館榮譽館長\n 國立臺中教育大學管理學院院長兼林之助紀念館館長\n 國立臺中教育大學文化創意產業設計與營運學系專任教授'
                        },
                        {
                            title: '專長',
                            text: '造型藝術、文化創意產業研究、公共藝術創作與研究'
                        },
                    ],
                },
            ],
        }
    },
    methods: {
        switchPlus() {
            ++this.count;
            if (this.count > 5) {
                this.count = 1;
            }
            console.log(this.count);

        },
        switchMinus() {
            --this.count;
            if (this.count < 1) {
                this.count = 5;
            }
            console.log(this.count);

        },
        switchContent() {
            switch (this.count) {
                case 1:
                    return 'transform: translateX(0%);'

                case 2:
                    return 'transform: translateX(calc(-1/5*100%));'

                case 3:
                    return 'transform: translateX(calc(-2/5*100%));'

                case 4:
                    return 'transform: translateX(calc(-3/5*100%));'

                case 5:
                    return 'transform: translateX(calc(-4/5*100%));'

                default:
                    return 'transform: translateX(0%);'
            }
        }
    },
}

</script>

<template>
    <div class="container mx-auto h-dvh md:h-[80dvh] mb-5 relative overflow-hidden">
        <!-- 
        包裹所有內容區，由左至右 可透過上面按鈕切換 -->
        <div class="wrap w-max h-full flex transition-transform" :style="this.switchContent()">

            <!-- 內容區塊-1 -->
            <div class="wrap w-dvw container h-full flex flex-col" v-for="content in contentData"
                :key="content.index">

                <!-- 標題 + 左右切換的按鈕 -->
                <div
                    class="intro-menu w-full h-[80px] flex-shrink-0 text-center text-2xl font-bold flex justify-center items-center relative">
                    <button type="button" class="absolute left-14 sm:left-1/4 md:left-1/3 w-5 h-full cursor-pointer"
                        @click="this.switchMinus">
                    <img src="../assets/img/down.png" alt="arrow" class="w-full rotate-90">
                    </button>

                    <h3 class="mx-6">{{ content.title }}</h3>

                    <button type="button" class="absolute right-14 sm:right-1/4 md:right-1/3 w-5 h-full cursor-pointer"
                        @click="this.switchPlus">
                        <img src="../assets/img/down.png" alt="arrow" class="w-full -rotate-90">
                    </button>

                </div>
                <!-- 下方內容區 左圖右文字md:2:3 lg:1:1 -->
                <div
                    class="wrap md:flex-grow w-[85%] h-[80dvh] md:w-full md:h-full mx-auto md:grid md:grid-cols-5 lg:grid-cols-2 overflow-y-auto overflow-x-clip md:overflow-hidden">
                    <!-- 圖片區 -->
                    <div id="intro-img" class="col-span-2 lg:col-span-1 flex flex-row justify-center items-start mb-3 md:mb-0">
                        <img class="h-[300px] md:h-full overflow-clip object-cover md:object-contain object-top" :src="content.img"
                            :alt="content.title">
                    </div>
                    <!-- 文字區 -->
                    <div class="col-span-3 lg:col-span-1 md:overflow-hidden">
                        <div id="intro-text"
                            class="w-full md:w-[80%] h-full md:mx-auto bg-[#D0C9BC]/60 md:overflow-y-auto md:overflow-x-clip p-3">
                            <div v-for="text in content.content" :key="text.title">
                                <h4 class="mb-1 text-lg font-bold">{{ text.title }}</h4>
                                <p class="mb-3 break-all whitespace-pre-line">{{ text.text }}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>


        </div>

    </div>
</template>
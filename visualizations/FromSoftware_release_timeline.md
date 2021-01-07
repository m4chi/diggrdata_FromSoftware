<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">  
        <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
        <title>Release Timeline</title>
        <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/d3/5.9.2/d3.js"></script>
        <link href="https://fonts.googleapis.com/css?family=Lora&display=swap" rel="stylesheet"> 
        <link href="https://fonts.googleapis.com/css?family=Archivo&display=swap" rel="stylesheet">
        <link href="https://fonts.googleapis.com/css?family=IBM+Plex+Serif&display=swap" rel="stylesheet">
        <link href="https://fonts.googleapis.com/css?family=Cairo&display=swap" rel="stylesheet"> 



        <style type="text/css">
            body {
                margin: 1em;
                font-size: 12px;
                font-family: 'Helvetica', 'Arial', sans-serif;
                font-family: 'Cairo', sans-serif;
                background: #faf5f9
            }       
            
            h1 {
                font-weight: 300;
                font-size: 45px;
                font-family: 'Cairo', sans-serif;
            }

            h3 {
                font-weight: 300;
                font-size: 30px;
                line-height: 38px;                
                margin-bottom: 20px;
                padding-bottom: 0px;
                padding-top: 0px;
                margin-top: 0px;
            }

            .curlyBracket {
                stroke: gray;
                stroke-width: 2px;
                fill: none;
            }            

            .tooltip {
                color: white;
                position: absolute;
                text-align: center;
                padding: 2px;
                font: 10px sans-serif;
                background: rgba(0,0,0,.6);
                pointer-events: none;
                border-radius: 3px;
            }        
            .boxart {
                float:left;
                height: 180px;
                width: 150px;
                background-color: white;
                margin-right: 20px;
                vertical-align: center;
            }

            .releaseDate {
                font-size: 14px;
                margin-bottom: 10px;
            }
            
            .gameTitle {
                font-size: 12px;
                font-weight: 300;
            }

            #gameDetails {
                position: absolute;
                width: 400px;
                line-height: 18px;
                border-right: 1px solid gray;
                border-left: 1px solid gray;
                height: 280px;
                border-radius: 10px;
                padding: 20px;
                opacity: 0;
                margin-top: 20px;
            }

            #gameSelectorDiv {
                float: right;
                margin-top: 50px;
            }
            #header {
                float: left;
            }

            select {
                width: 400px;
                border: 0px solid gray;
                font-size: 20px;
                color: afafaf;
                padding: 10px;
                border-radius: 3px
            }

            select option {
                width: 400px;
                font-size: 15px;
                color: afafaf;
                padding: 10px;                
            }


            .main-svg {
                
            }
        </style>

    </head>
    <body>
        <div id="header">
            <h1>Release Timeline</h1>
        </div>
        <div id="gameSelectorDiv">

        </div>

        <div id="svg"></div>
        <div id="gameDetails"></div>




        <script type="text/javascript">


            const dataset = JSON.parse(
                '[["3D Dot Game Heroes", [{"title": "3D Dot Game Heroes", "date": "2009-11-05T00:00:00", "region": "JP"}, {"title": "3D Dot Game Heroes", "date": "2010-05-11T00:00:00", "region": "US"}, {"title": "3D Dot Game Heroes", "date": "2010-05-14T00:00:00", "region": "EU"}], ""], ["ARMORED CORE MASTER OF ARENA", [{"title": "Armored Core: Master of Arena", "date": "1999-02-04T00:00:00", "region": "JP"}, {"title": "Armored Core: Master of Arena", "date": "2000-02-29T00:00:00", "region": "US"}], ""], ["ARMORED CORE PROJECT PHANTASMA", [{"title": "Armored Core: Project Phantasma", "date": "1997-12-04T00:00:00", "region": "JP"}, {"title": "Armored Core: Project Phantasma", "date": "1998-09-30T00:00:00", "region": "US"}], ""], ["Adventure Player", [{"title": "Adventure Player", "date": "2005-06-30T00:00:00", "region": "JP"}], ""], ["Armored Core", [{"title": "Armored Core", "date": "1997-07-10T00:00:00", "region": "JP"}, {"title": "Armored Core", "date": "1997-10-31T00:00:00", "region": "US"}, {"title": "Armored Core", "date": "1998-07-01T00:00:00", "region": "EU"}], ""], ["Armored Core 2", [{"title": "Armored Core 2", "date": "2000-08-03T00:00:00", "region": "JP"}, {"title": "Armored Core 2", "date": "2000-10-24T00:00:00", "region": "US"}, {"title": "Armored Core 2", "date": "2001-03-23T00:00:00", "region": "EU"}], ""], ["Armored Core 2: Another Age", [{"title": "Armored Core 2: Another Age", "date": "2001-04-12T00:00:00", "region": "JP"}, {"title": "Armored Core 2: Another Age", "date": "2001-08-20T00:00:00", "region": "US"}, {"title": "Armored Core 2: Another Age", "date": "2002-09-27T00:00:00", "region": "EU"}], ""], ["Armored Core 3", [{"title": "Armored Core 3", "date": "2002-04-04T00:00:00", "region": "JP"}, {"title": "Armored Core 3", "date": "2002-09-05T00:00:00", "region": "US"}, {"title": "Armored Core 3", "date": "2003-05-30T00:00:00", "region": "EU"}], ""], ["Armored Core 4", [{"title": "Armored Core 4", "date": "2006-12-21T00:00:00", "region": "JP"}, {"title": "Armored Core 4", "date": "2007-03-20T00:00:00", "region": "US"}, {"title": "Armored Core 4", "date": "2007-06-22T00:00:00", "region": "EU"}], ""], ["Armored Core V", [{"title": "Armored Core V", "date": "2012-01-26T00:00:00", "region": "JP"}, {"title": "Armored Core V", "date": "2012-03-20T00:00:00", "region": "US"}, {"title": "Armored Core V", "date": "2012-03-23T00:00:00", "region": "EU"}], ""], ["Armored Core: For Answer", [{"title": "Armored Core: For Answer", "date": "2008-03-19T00:00:00", "region": "JP"}, {"title": "Armored Core: For Answer", "date": "2008-09-16T00:00:00", "region": "US"}, {"title": "Armored Core: For Answer", "date": "2008-11-28T00:00:00", "region": "EU"}], ""], ["Armored Core: Formula Front - Extreme Battle", [{"title": "Armored Core: Formula Front", "date": "2004-12-12T00:00:00", "region": "JP"}, {"title": "Armored Core: Formula Front - Extreme Battle", "date": "2005-12-15T00:00:00", "region": "US"}, {"title": "Armored Core: Formula Front - Extreme Battle", "date": "2006-03-03T00:00:00", "region": "EU"}], ""], ["Armored Core: Last Raven", [{"title": "Armored Core: Last Raven", "date": "2005-08-04T00:00:00", "region": "JP"}, {"title": "Armored Core: Last Raven", "date": "2006-06-13T00:00:00", "region": "US"}, {"title": "Armored Core: Last Raven", "date": "2006-10-06T00:00:00", "region": "EU"}], ""], ["Armored Core: Machine Side Box", [], ""], ["Armored Core: Nexus", [{"title": "Armored Core: Nexus", "date": "2004-03-18T00:00:00", "region": "JP"}, {"title": "Armored Core: Nexus", "date": "2004-09-28T00:00:00", "region": "US"}, {"title": "Armored Core: Nexus", "date": "2006-04-13T00:00:00", "region": "EU"}], ""], ["Armored Core: Nine Breaker", [{"title": "Armored Core: Nine Breaker", "date": "2004-10-28T00:00:00", "region": "JP"}, {"title": "Armored Core: Nine Breaker", "date": "2005-09-13T00:00:00", "region": "US"}, {"title": "Armored Core: Nine Breaker", "date": "2006-05-05T00:00:00", "region": "EU"}], ""], ["Armored Core: Verdict Day", [{"title": "Armored Core: Verdict Day", "date": "2013-09-26T00:00:00", "region": "JP"}, {"title": "Armored Core: Verdict Day", "date": "2013-09-24T00:00:00", "region": "US"}, {"title": "Armored Core: Verdict Day", "date": "2013-09-27T00:00:00", "region": "EU"}], ""], ["Bloodborne", [{"title": "Bloodborne", "date": "2015-03-26T00:00:00", "region": "JP"}, {"title": "Bloodborne", "date": "2015-03-24T00:00:00", "region": "US"}, {"title": "Bloodborne", "date": "2015-03-27T00:00:00", "region": "EU"}], ""], ["Cookie & Cream", [{"title": "KuriKuri DS: Otasuke Island", "date": "2007-06-28T00:00:00", "region": "JP"}, {"title": "Cookie & Cream", "date": "2007-07-02T00:00:00", "region": "US"}, {"title": "Cookie & Cream", "date": "2007-10-05T00:00:00", "region": "EU"}], ""], ["DARK SOULS II", [{"title": "Dark Souls II", "date": "2014-03-13T00:00:00", "region": "JP"}, {"title": "Dark Souls II", "date": "2014-03-11T00:00:00", "region": "US"}, {"title": "Dark Souls II", "date": "2014-03-14T00:00:00", "region": "EU"}], ""], ["DARK SOULS III", [{"title": "Dark Souls III", "date": "2016-03-24T00:00:00", "region": "JP"}, {"title": "Dark Souls III", "date": "2016-04-12T00:00:00", "region": "US"}, {"title": "Dark Souls III", "date": "2016-04-12T00:00:00", "region": "EU"}], ""], ["Dark Souls", [{"title": "Dark Souls", "date": "2011-09-22T00:00:00", "region": "JP"}, {"title": "Dark Souls", "date": "2011-10-04T00:00:00", "region": "US"}, {"title": "Dark Souls", "date": "2011-10-07T00:00:00", "region": "EU"}], ""], ["Dark Souls II: Scholar of the First Sin", [{"title": "Dark Souls II: Scholar of the First Sin", "date": "2015-02-05T00:00:00", "region": "JP"}, {"title": "Dark Souls II: Scholar of the First Sin", "date": "2015-04-07T00:00:00", "region": "US"}, {"title": "Dark Souls II: Scholar of the First Sin", "date": "2015-04-02T00:00:00", "region": "EU"}], ""], ["Dark Souls: Artorias of the Abyss", [{"title": "Dark Souls: Artorias of the Abyss", "date": "2012-10-23T00:00:00", "region": "US"}], ""], ["Dark Souls: Remastered", [], ""], ["Demon\'s Souls", [{"title": "Demon\'s Souls", "date": "2009-02-05T00:00:00", "region": "JP"}, {"title": "Demon\'s Souls", "date": "2009-10-06T00:00:00", "region": "US"}, {"title": "Demon\'s Souls (Black Phantom Edition)", "date": "2010-06-25T00:00:00", "region": "EU"}], ""], ["Deracine", [], ""], ["ECHO NIGHT\\uff032 \\u7720\\u308a\\u306e\\u652f\\u914d\\u8005", [{"title": "Echo Night #2: Nemuri no Shihaisha", "date": "1999-08-05T00:00:00", "region": "JP"}], ""], ["Echo Night", [{"title": "Echo Night", "date": "1998-08-13T00:00:00", "region": "JP"}, {"title": "Echo Night", "date": "1999-07-31T00:00:00", "region": "US"}], ""], ["Echo Night: Beyond", [{"title": "Nebula: Echo Night", "date": "2004-01-22T00:00:00", "region": "JP"}, {"title": "Echo Night Beyond", "date": "2004-07-27T00:00:00", "region": "US"}, {"title": "Echo Night Beyond", "date": "2005-08-26T00:00:00", "region": "EU"}], ""], ["Enchanted Arms", [{"title": "[eM] -eNCHANT arM-", "date": "2006-01-12T00:00:00", "region": "JP"}, {"title": "Enchanted Arms", "date": "2006-08-29T00:00:00", "region": "US"}, {"title": "Enchanted Arms", "date": "2006-09-08T00:00:00", "region": "EU"}], ""], ["EverGrace", [{"title": "Evergrace", "date": "2000-04-27T00:00:00", "region": "JP"}, {"title": "Evergrace", "date": "2000-10-24T00:00:00", "region": "US"}, {"title": "Evergrace", "date": "2001-03-30T00:00:00", "region": "EU"}], ""], ["FRAME GRIDE", [{"title": "Frame Gride", "date": "1999-07-15T00:00:00", "region": "JP"}], ""], ["Forever Kingdom", [{"title": "Evergrace II", "date": "2001-06-21T00:00:00", "region": "JP"}, {"title": "Forever Kingdom", "date": "2002-01-21T00:00:00", "region": "US"}], ""], ["Fuuun Shinsengumi Bakumatsuden Portable", [{"title": "Fuuun Shinsengumi Bakumatsuden Portable", "date": "2009-12-10T00:00:00", "region": "JP"}], ""], ["Inugamike no Ichizoku", [{"title": "Inugamike no Ichizoku", "date": "2009-01-22T00:00:00", "region": "JP"}], ""], ["King\'s Field", [{"title": "King\'s Field", "date": "1994-12-16T00:00:00", "region": "JP"}], ""], ["King\'s Field 4", [{"title": "King\'s Field IV", "date": "2001-10-04T00:00:00", "region": "JP"}, {"title": "King\'s Field: The Ancient City", "date": "2002-03-25T00:00:00", "region": "US"}, {"title": "King\'s Field IV", "date": "2003-03-28T00:00:00", "region": "EU"}], ""], ["King\'s Field II", [{"title": "King\'s Field II", "date": "1995-07-21T00:00:00", "region": "JP"}, {"title": "King\'s Field (Long Box)", "date": "1995-12-31T00:00:00", "region": "US"}, {"title": "King\'s Field", "date": "1996", "region": "EU"}], ""], ["King\'s Field III", [{"title": "King\'s Field III (Power Completist)", "date": "1996", "region": "JP"}, {"title": "King\'s Field II", "date": "1996-10-31T00:00:00", "region": "US"}], ""], ["King\'s Field: Additional I", [{"title": "King\'s Field: Additional I", "date": "2006-07-20T00:00:00", "region": "JP"}], ""], ["King\'s Field: Additional II", [{"title": "King\'s Field: Additional II", "date": "2006-08-24T00:00:00", "region": "JP"}], ""], ["Kuon", [{"title": "Kuon", "date": "2004-04-01T00:00:00", "region": "JP"}, {"title": "Kuon", "date": "2004-12-07T00:00:00", "region": "US"}, {"title": "Kuon", "date": "2006-04-28T00:00:00", "region": "EU"}], ""], ["Lost Kingdoms", [{"title": "Rune", "date": "2002-04-25T00:00:00", "region": "JP"}, {"title": "Lost Kingdoms", "date": "2002-05-27T00:00:00", "region": "US"}, {"title": "Lost Kingdoms", "date": "2002-08-09T00:00:00", "region": "EU"}], ""], ["Lost Kingdoms II", [{"title": "Rune II: Koruten no Kagi no Himitsu", "date": "2003-05-23T00:00:00", "region": "JP"}, {"title": "Lost Kingdoms II", "date": "2003-05-21T00:00:00", "region": "US"}, {"title": "Lost Kingdoms II", "date": "2003-06-06T00:00:00", "region": "EU"}], ""], ["Metal Wolf Chaos", [{"title": "Metal Wolf Chaos", "date": "2004-12-22T00:00:00", "region": "JP"}], ""], ["Murakumo: Renegade Mech Pursuit", [{"title": "Murakumo", "date": "2002-07-25T00:00:00", "region": "JP"}, {"title": "Murakumo: Renegade Mech Pursuit", "date": "2003-03-05T00:00:00", "region": "US"}], ""], ["Otogi: Myth of Demons", [{"title": "Otogi", "date": "2002-12-12T00:00:00", "region": "JP"}, {"title": "Otogi: Myth of Demons", "date": "2003-08-27T00:00:00", "region": "US"}, {"title": "Otogi: Myth of Demons", "date": "2003-09-05T00:00:00", "region": "EU"}], ""], ["O\\u30fbTO\\u30fbGI \\uff5e\\u767e\\u9b3c\\u8a0e\\u4f10\\u7d75\\u5dfb\\uff5e", [{"title": "Otogi: Hyakki Toubatsu Emaki", "date": "2003-12-25T00:00:00", "region": "JP"}, {"title": "Otogi 2: Immortal Warriors", "date": "2004-10-21T00:00:00", "region": "US"}, {"title": "Otogi 2: Immortal Warriors", "date": "2005-02-11T00:00:00", "region": "EU"}], ""], ["SPRIGGAN -LUNAR VERSE-", [{"title": "Spriggan: Lunar Verse", "date": "1999-06-17T00:00:00", "region": "JP"}], ""], ["Sekiro: Shadows Die Twice", [], ""], ["Shadow Assault Tenchu", [{"title": "Shadow Assault -Tenchu-", "date": "2008-10-08T00:00:00", "region": "JP"}, {"title": "Shadow Assault -Tenchu-", "date": "2008-10-08T00:00:00", "region": "US"}, {"title": "Shadow Assault -Tenchu-", "date": "2008-10-08T00:00:00", "region": "EU"}], ""], ["Shadow Tower", [{"title": "Shadow Tower", "date": "1998-06-25T00:00:00", "region": "JP"}, {"title": "Shadow Tower", "date": "1999-10-31T00:00:00", "region": "US"}], ""], ["Shadow Tower: Abyss", [{"title": "Shadow Tower: Abyss", "date": "2003-10-23T00:00:00", "region": "JP"}], ""], ["Silent Line: Armored Core", [{"title": "Armored Core 3: Silent Line", "date": "2003-01-23T00:00:00", "region": "JP"}, {"title": "Silent Line: Armored Core", "date": "2003-07-17T00:00:00", "region": "US"}, {"title": "Silent Line: Armored Core", "date": "2005-07-01T00:00:00", "region": "EU"}], ""], ["Steel Battalion: Heavy Armor", [{"title": "Jutekki: Steel Batallion", "date": "2012-06-21T00:00:00", "region": "JP"}, {"title": "Steel Battalion: Heavy Armor", "date": "2012-06-19T00:00:00", "region": "US"}, {"title": "Steel Battalion: Heavy Armor", "date": "2012-06-22T00:00:00", "region": "EU"}], ""], ["Tenchu Z", [{"title": "Tenchu Senran", "date": "2006-10-05T00:00:00", "region": "JP"}, {"title": "Tenchu Z", "date": "2007-06-12T00:00:00", "region": "US"}, {"title": "Tenchu Z", "date": "2007-06-29T00:00:00", "region": "EU"}], ""], ["Tenchu: Dark Secret", [{"title": "Tenchu: Dark Shadow", "date": "2006-04-06T00:00:00", "region": "JP"}, {"title": "Tenchu: Dark Secret", "date": "2006-08-21T00:00:00", "region": "US"}, {"title": "Tenchu: Dark Secret", "date": "2006-11-24T00:00:00", "region": "EU"}], ""], ["Tenchu: Fatal Shadows", [{"title": "Tenchu Kurenai", "date": "2004-07-22T00:00:00", "region": "JP"}, {"title": "Tenchu: Fatal Shadows", "date": "2005-02-15T00:00:00", "region": "US"}, {"title": "Tenchu: Fatal Shadows", "date": "2005-05-06T00:00:00", "region": "EU"}], ""], ["Tenchu: Shadow Assassins", [{"title": "Tenchu 4", "date": "2008-10-23T00:00:00", "region": "JP"}, {"title": "Tenchu: Shadow Assassins", "date": "2009-02-05T00:00:00", "region": "US"}, {"title": "Tenchu: Shadow Assassins", "date": "2009-03-12T00:00:00", "region": "EU"}], ""], ["Tenchu: Time of the Assassins", [{"title": "Tenchu: Shinobi Taizen", "date": "2005-07-28T00:00:00", "region": "JP"}, {"title": "Tenchu: Time of the Assassins", "date": "2006-06-23T00:00:00", "region": "EU"}], ""], ["The Adventures of Cookie & Cream", [{"title": "Kuri Kuri Mix", "date": "2000-12-07T00:00:00", "region": "JP"}, {"title": "The Adventures of Cookie & Cream", "date": "2001-04-30T00:00:00", "region": "US"}, {"title": "Kuri Kuri Mix", "date": "2001-05-04T00:00:00", "region": "EU"}], ""], ["Yatsu Hakamura", [{"title": "Yatsu Hakamura", "date": "2009-04-23T00:00:00", "region": "JP"}], ""], ["Yoshitsune Eiyuuden", [{"title": "Yoshitsune Eiyuuden: The Story of Hero Yoshitsune", "date": "2005-01-13T00:00:00", "region": "JP"}], ""], ["\\u30a4\\u30e9\\u30ed\\u30b8VOW", [{"title": "Iraroji VOW", "date": "2007-05-24T00:00:00", "region": "JP"}], ""], ["\\u30b5\\u30a6\\u30b6\\u30f3\\u30c9\\u30e9\\u30f3\\u30c9 Thousand Land", [{"title": "Thousand Land", "date": "2003-03-20T00:00:00", "region": "JP"}], ""], ["\\u30cb\\u30f3\\u30b8\\u30e3\\u30d6\\u30ec\\u30a4\\u30c9", [{"title": "Ninja Blade", "date": "2009-01-29T00:00:00", "region": "JP"}, {"title": "Ninja Blade", "date": "2009-04-07T00:00:00", "region": "US"}, {"title": "Ninja Blade", "date": "2009-04-03T00:00:00", "region": "EU"}], ""], ["\\u5929\\u8a85 \\u53c2", [{"title": "Tenchu San", "date": "2003-04-24T00:00:00", "region": "JP"}, {"title": "Tenchu: Wrath of Heaven", "date": "2003-03-03T00:00:00", "region": "US"}, {"title": "Tenchu: Wrath of Heaven", "date": "2003-03-07T00:00:00", "region": "EU"}], ""], ["\\u5df1\\u306e\\u4fe1\\u305a\\u308b\\u9053\\u3092\\u5f81\\u3051", [{"title": "Onore no Shinzuru Michi o Yuke", "date": "2009-06-11T00:00:00", "region": "JP"}], ""]]'
            )
            const years = JSON.parse(
                '[1994, 1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016]'
            )

            // Helper functions
            
            // curly bracket function: http://bl.ocks.org/alexhornbake/6005176
            function makeCurlyBrace(x1,y1,x2,y2,w,q)
            {
                //Calculate unit vector
                var dx = x1-x2;
                var dy = y1-y2;
                var len = Math.sqrt(dx*dx + dy*dy);
                dx = dx / len;
                dy = dy / len;
    
                //Calculate Control Points of path,
                var qx1 = x1 + q*w*dy;
                var qy1 = y1 - q*w*dx;
                var qx2 = (x1 - .25*len*dx) + (1-q)*w*dy;
                var qy2 = (y1 - .25*len*dy) - (1-q)*w*dx;
                var tx1 = (x1 -  .5*len*dx) + w*dy;
                var ty1 = (y1 -  .5*len*dy) - w*dx;
                var qx3 = x2 + q*w*dy;
                var qy3 = y2 - q*w*dx;
                var qx4 = (x1 - .75*len*dx) + (1-q)*w*dy;
                var qy4 = (y1 - .75*len*dy) - (1-q)*w*dx;
    
                return ( "M " +  x1 + " " +  y1 +
                        " Q " + qx1 + " " + qy1 + " " + qx2 + " " + qy2 + 
                        " T " + tx1 + " " + ty1 +
                        " M " +  x2 + " " +  y2 +
                        " Q " + qx3 + " " + qy3 + " " + qx4 + " " + qy4 + 
                        " T " + tx1 + " " + ty1 );
            }



            function initVis(w, h, containerName) {
                const vis = d3.select('#'+containerName)
                    .append('svg')
                        .attr('class', 'main-svg')
                        .attr('width', w)
                        .attr('height', h)
                return vis
            }

            function initTooltip() {
                // prepare tooltip element
                const tooltip = d3.select("body").append('div')
                    .attr('class', 'tooltip')
                    .style('opacity', 0)
                return tooltip
            }
            function resetTooltip(tp) {
                tp
                    .transition()
                    .duration(100)
                    .style('opacity', 0);                
            }

            function getParentNodeData(n) {
                return d3.select(n.parentNode).node().__data__
            }

            function timelineBackground(svg, years, h) {
                const bg = vis.selectAll('.bg')
                    .data(years)
                    .enter().append('rect')
                        .attr('fill', (d) => d%2 === 0 ? '#faf5f9' : 'white' )
                        .attr('x', (d) => {  return x(d3.isoParse(d.toString()+"-1-1")) })
                        .attr('y', 30)
                        .attr('height', h-50)
                        .attr('width', (d) => {
                            return xValue = x(d3.isoParse((d+1).toString()+"-01-01"))-x(d3.isoParse(d.toString()+"-01-1"))
                        })                        

                const yearLabels = vis.selectAll('g.yearLabels')
                .data(allYears)
                .enter().append('text')
                    .text((d) => d)
                    .style('font-size', 11)
                    .attr('x', (d) => 6+x(d3.isoParse(d.toString()+"-1-1")))
                    .attr('y', 25)

            }

            function normalizeDate(yearString) {
                if (yearString.length === 4) {
                    return d3.isoParse(yearString+"-1-1")
                }
                else {
                    return d3.isoParse(yearString)
                }
            }

            // SETUP
            const W = 1900
            const H = 300
            const offset = 70

            const releaseMarkerColors = {
                JP: "red",
                US: "blue",
                EU: "green"
            }

            //const years = d3.range(1993, 2020)
            const regions = [ 'US', 'JP', 'EU']

            const allYears = d3.range(d3.min(years)-1, d3.max(years)+2)

            // SCALES
            const x = d3.scaleTime()
                .domain([ new Date(d3.min(years)-1, 0, 1), new Date(d3.max(years)+2, 0 ,1)])
                .range([0, W])                
            const y = d3.scaleOrdinal()
                .domain(regions)
                .range(d3.range(offset, H, (H-offset*2)/(regions.length-1)))


            // Initialize svg
            const vis = initVis(W, H, 'svg')
            timelineBackground(vis, years, H)
            const tooltip = initTooltip()
            const gameDetails = d3.select('#gameDetails')


            // Add visualization elements
            const regionTimeline = vis.selectAll('.regions') 
                .data(regions)
                .enter().append('g')

            regionTimeline.append('text')
                .attr('x', 6)
                .attr('y', (d) => y(d) - 3)
                .text((d) => d)
                .style('font-size', '11px')
                .attr('fill', (d) => releaseMarkerColors[d])


            regionTimeline.append('rect')
                .attr('x', 0)
                .attr('y', (d) => y(d))
                .attr('width', W)
                .attr('height', 1)
                .attr('fill', (d) => releaseMarkerColors[d])
                .style('opacity', '0.3')

            

            function  releaseArea2(r1, r2) {
                let points = [
                    //[x(normalizeDate(r1.date)), y(r1.region)],
                    //[x(normalizeDate(r2.date)), y(r2.region)],
                    //[x(normalizeDate(r1.date)), y(r2.region)]
                    [x(normalizeDate(r1.date)), y(r1.region)],
                    [x(normalizeDate(r2.date)), y(r2.region)],
                    [x(normalizeDate(r2.date))+4, y(r2.region)],
                    [x(normalizeDate(r1.date))+4, y(r1.region)],

                ]
                points = points.map((d) => d.join(',')).join(' ')    
                return points             
            }

            function releaseArea3(rList) {
                const [ r1, r2, r3 ] = rList
                let points = [
                    //[x(normalizeDate(r1.date)), y(r1.region)],
                    //[x(normalizeDate(r2.date))+1, y(r2.region)],
                    //[x(normalizeDate(r1.date))+1, y(r2.region)],
                    //[x(normalizeDate(r1.date)), y(r1.region)],
                    //[x(normalizeDate(r3.date))+1, y(r3.region)],
                    //[x(normalizeDate(r1.date))+1, y(r3.region)]
                    [x(normalizeDate(r1.date)), y(r1.region)],
                    [x(normalizeDate(r2.date)), y(r2.region)],
                    [x(normalizeDate(r3.date)), y(r3.region)],
                ]     
                points = points.map((d) => d.join(',')).join(' ')         
                return points         
            }

            function releaseAreaPoints(releases) {
                let points = ""
                jp = releases.filter((d) => d.region === 'JP' ? d : null)[0]
                eu = releases.filter((d) => d.region === 'EU' ? d : null)[0]
                us = releases.filter((d) => d.region === 'US' ? d : null)[0]                
                if (releases.length === 2) {
                    if (!jp) 
                        points = releaseArea2(eu, us)
                    else if (!eu)
                        points = releaseArea2(jp, us)
                    else if (!us) 
                        points = releaseArea2(jp, eu)                  
                }
                else if (releases.length === 3) {
                    jp = releases.filter((d) => d.region === 'JP' ? d : null)[0]
                    eu = releases.filter((d) => d.region === 'EU' ? d : null)[0]
                    us = releases.filter((d) => d.region === 'US' ? d : null)[0]
                    console.log([jp, eu, us])
                    console.log([jp, eu, us].sort())
                    points =releaseArea3([jp, eu, us].sort((item, other) => item.date > other.date ? 1 : 0))             
                }
                return points
            }
            

            const areas = vis.selectAll('.release_area')
                .data(dataset).enter().append('g')
                .append('polygon')
                    .attr('points', (d) => releaseAreaPoints(d[1]))
                    .attr('fill' ,'teal')
                    .style('opacity', 0.05)

            const games = vis.selectAll('.games')
                .data(dataset)
                .enter().append('g')

            const boxartImageLink = (url) => {
                if (url !== "")
                    return "<img src='"+url+"' width='150' />"
                else
                    return "&nbsp;&nbsp;no boxart available"
            }

            const getGameDetailsPosition = (data) => {
                let dates = data.map((item) => item.date)
                dates = dates.sort()

                let pos = Math.round(x(normalizeDate(dates[0]))) - 15
                if ((pos+400) > W) {
                    pos = W - 440
                }
                return pos.toString()+"px"
            }

            const getBracketXPosition = (data) => {
                let dates = data.map((item) => item.date)
                dates = dates.sort()
                return {
                    start: x(normalizeDate(dates[0])) - 10,
                    end: x(normalizeDate(dates[dates.length-1])) + 10
                }
            }


            function updateSelectedGame(data) {

                d3.selectAll('.selectedReleaseArea')
                    .remove()
                const releaseArea = vis.append('g')
                releaseArea.append('polygon')
                    .attr('points', (d) => releaseAreaPoints(data[1]))
                    .attr('fill' ,'teal')
                    .style('opacity', 0.5)
                    .attr('class', 'selectedReleaseArea')

                d3.selectAll('.curlyBracket')
                    .remove()
                const bracketX = getBracketXPosition(data[1])
                const bracket = vis.append('g')                       
                bracket.append('path')
                    .attr('class', 'curlyBracket')
                    .attr("d", (d) => makeCurlyBrace(bracketX.start,255,bracketX.end,255,10,0.6))
                
                gameDetails
                    .html('')


                gameDetails
                    .style('left', getGameDetailsPosition(data[1]))
                    .style('top', '440px')   
                    .style('opacity', 1.0)                     
                    .html(
                        "<div><h3>"+data[0]+"</h3></div>"+
                        "<div class='boxart'>"+
                        boxartImageLink(data[2])+
                        "</div>"+
                        "<div class="
                        
                    )

                gameDetails.selectAll('.releases')
                    .data(data[1])
                    .enter().append('div')
                        .attr('class', 'releaseDate')
                        .html((d) =>  
                            "First "+d.region+" Release: "+d.date.substring(0,10)+
                            "<br /><span class='gameTitle'>"+d.title+"</span>"
                        )
                    
                d3.selectAll('.selectedGame')
                    .remove()

                const currentGame = vis.selectAll(".selectedGame")
                    .data(data[1])
                    .enter().append("circle")
                        .attr('class', 'selectedGame')
                        .attr('cx', (d) => {  return x(normalizeDate(d.date)) })
                        .attr('cy', (d) => y(d.region))
                        .attr('r', 8)
                        .attr('fill', (d) => releaseMarkerColors[d.region])                             

            }


            const releaseMarkers = games.selectAll('.releases')
                .data((d) => d[1])
                .enter().append('circle')
                    .attr('cx', (d) => { return x(normalizeDate(d.date)) })
                    .attr('cy', (d) => y(d.region))
                    .attr('r', 3)
                    .attr('fill', (d) => releaseMarkerColors[d.region])
                    .style('opacity', 0.5)
                    .on('mouseover', function(i) {

                        const parentNodeData = d3.select(this.parentNode).node().__data__
                        const data = parentNodeData[1].filter((item) => {
                            if (item.date != i.date)
                                return item
                        })
                    
                        const currentGame = vis.selectAll(".currentGame")
                            .data(data)
                            .enter().append("circle")
                                .attr('class', 'currentGame')
                                .attr('cx', (d) => {  return x(normalizeDate(d.date)) })
                                .attr('cy', (d) => y(d.region))
                                .attr('r', 8)
                                .attr('fill', (d) => releaseMarkerColors[d.region])   
                                .style('opacity', '0.5')                         

                        d3.select(this)
                            .transition()
                            .duration(200)
                            .attr('r', 8) 
                            .style('cursor', 'pointer')
                        tooltip
                            .transition()
                            .duration(100)
                            .style('opacity', 0.9)
                        tooltip
                            .html(i.title+"<br />"+i.date.substring(0,10))
                            .style('left', d3.event.pageX + 10 + 'px')
                            .style('top', d3.event.pageY - 38 + 'px');                               
                    })
                    .on('mouseout', function(i) {
                        d3.select(this)
                            .transition()
                            .duration(200)
                            .attr('r', 3)      
                        resetTooltip(tooltip)     
                        d3.selectAll('.currentGame')
                            .remove()
                    })
                    .on('click', function(i) {
                        const data = getParentNodeData(this)
                        
                        updateSelector(data[0])
                        updateSelectedGame(data)
                    })

                //game selector

                function normalizeGameTitle(title) {
                    return title.replace(/[^\w]/g, '')
                }

                function updateSelector(gameTitle) {
                    const select = d3.select('#selectId')
                    select.node().value = gameTitle
                }

                const gameTitles = dataset.map((item) => item[0])

                const gameSelector = d3.select('#gameSelectorDiv')
                    .append('select')
                        .attr('id', 'selectId')
                gameSelector.append('option')
                    .attr('value', 'Select game')
                    .attr('disabled', true)
                    .attr('selected', true)
                    .html('Select game')
                    
                
                gameSelector.selectAll('.selectOption')
                    .data(gameTitles.sort())
                    .enter().append('option') 
                        .attr('id', (d) => "o_"+normalizeGameTitle(d) )
                        .attr('value', (d) => d)
                        .html((d) => d)
                    .on('click', function(i) {
                        const data = dataset.filter((e) => e[0] === i ? e : null)[0]
                        updateSelectedGame(data)
                    })


            </script>

    </body>
</html>
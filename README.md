# HTML-movie
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://code.jquery.com/jquery-3.7.1.js"></script>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL"
        crossorigin="anonymous"></script>
    <title>일별 박스오피스</title>
    <script src="https://code.jquery.com/jquery-3.7.1.js"> </script>
    <script>
        let key ='7f7314005c9a1bb8ee535cedbd043a27'
        let api_url = 'http://kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json'
        $(document).ready(function(){
            $("#btn").click(function(){
                let st = $("#st").val().replaceAll('-','');
                console.log(st);
                $.ajax({
                    url:api_url
                    ,data : {key : key, targetDt:st}
                    ,type : 'GET'
                    ,dataType : 'json'
                    ,success: function (res){
                        // console.log(res);
                        let str=''
                        let arr = res['boxOfficeResult']['dailyBoxOfficeList']
                        $.each(arr,function(i,v){
                            str += '<tr>'
                            str += '<td>' + v['rank'] + '</td>'
                            str += '<td>' + v['movieNm'] + '</td>'
                            str += '<td>' + v['openDt'] + '</td>'
                            str += '<td>' + v['salesAmt'] + '</td>'
                            str += '<td>' + v['salesAcc'] + '</td>'
                            str += '<td>' + v['audiCnt'] + '</td>'
                            str += '<td>' + v['audiAcc'] + '</td>'
                            str += '<td>' + v['scrnCnt'] + '</td>'
                            str += '</tr>'
                        })
                        $('#tbl').append(str);
                    },error:function(e){
                        console.log(e);
                    }
                })
            });
        });
        
    </script>
</head>
<body>
    <div class="row pt-5">
        <div class="col-md-4"></div>
        <div class="col-md-4">
            <div class="input-group">
                <span class="input-group-text">검색</span>
                <input type="date"  id="st" aria-label="First name" class="form-control">
                <button id="btn" class="btn btn-dark">조회</button>
            </div>
        </div>
        <div class="col-md-4"></div>
        
    </div>
    <div class="row pt-1">
        <div class="col-md-2"></div>
        <div class="col-md-8">
            <table class="table table-dark table-striped table-hover">
                <thead>
                    <tr><td>순위</td>
                        <td class="center">영화명</td>
                        <td>개봉일</td>
                        <td>매출액</td>
                        <td>누적 매출액</td>
                        <td>관괙수</td>
                        <td>누적 관객수</td>
                        <td>당일 스크린 수</td>
                    </tr>
                </thead>
                <tbody id="tbl">
                </tbody>
            </table>
        </div>
        <div class="col-md-2"></div>
    </div>
    <div class="row"></div>

 
</body>
</html>

---
layout: amp
title: "Community Controller"
description: "Community Controller"
tag: [Codeigniter]
category: develope
sitemap:
  changefreq: daily
---
Commnuity 컨트롤러에 게시물 관련 클래스

```java
private function construct_event_boarding($data){
  $__onLoadScripts = $this->load->get_var('__onLoadScripts');

  $script = ""; $loadscript = "";
  if( !isset($_POST['mode']) ){ // post로 넘어오는 mode값이 없으면
    //board.common.js 스크립트 호출해서 목록을 출력할 수 있도록...list로 초기화
    $this->output->append_output("<script type='text/javascript'>boardloadurl='/community/event';</script><script type='text/javascript' src='/js/board.common.js'></script>");
    $loadscript .= 'jQuery.extend( true, (window.board||(window.board={})), { funcs_config:{';
    $loadscript .= 'list: function(){
      var self = this.data("board");
      self.args("args.mode", "list", true);
      self.load();
    }';
    $loadscript .= '}});';
    $loadscript .= 'window.resizeEventArray.push(board.funcs("resizeimg", $("#list")));'; //resizeimg함수객체를! resizeimg: function($p=>#list)
    //$__onLoadScripts에 $loadscript 추가
    array_push($__onLoadScripts, $loadscript);
  }else{
    if( $_POST['mode']==='list' ){  
      $this->append_list_basescripts($data,  array('board.resizeimgwidth=0;board.funcs("resizeimg", $("#list"));'));

    }else if(  $_POST['mode']==='view'  ){
      $data = new Data($data);
      if( !$data->get('no') ){ // 게시물을 데이터로 못갖고오면
        echo '<script type="text/javascript">';
        echo '$km.alert("존재하지 않는 게시글입니다.", function(){ board.funcs("list"); });';
        echo '</script>';
        exit;//종료
      }
    }
  }
  $this->load->vars('__onLoadScripts', $__onLoadScripts);
}
```

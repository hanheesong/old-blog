---
layout: amp
title: "코드이그나이터 Controller _remap() real contents"
description: "코드이그나이터 index.php"
tag: [php, 코드이그나이터]
category: develope
sitemap:
  changefreq: daily
---

```javascript
public function _remap(){
		$args = func_get_args(); //함수의 인수 목록을 구성하는 배열을 반환
		$data = call_user_func_array( array($this,'_remap_Revolution'), $args);
		return;
    //함수, 함수
		$method = array_shift($args);
		$classname = strtolower($this->curclassname());


		#	create head
		$this->CI()->print_including('head', "{$classname}.{$method}");
		#	create header
		$this->CI()->print_including('header', "{$classname}.{$method}");

		#	start create real contents
		$data = array();
		$data['curmenu'] = $classname;
		$data['cursubmenu'] = strtolower($method);
		if( property_exists($this, 'mainmodel') && is_callable(array($this->mainmodel, '__init')) ){
			$result = call_user_func_array(array($this->mainmodel, '__init'), $args);
			if( !is_array($result) ) $result = array();
			$data = array_merge($data, $result);
			if( $data['cursubmenu']==='index' && isset($data['default']) ){
				$data['cursubmenu'] = $method = $data['default'];
			}
		}
		if( property_exists($this, 'mainmodel') && is_callable(array($this->mainmodel, $method)) ){
			$result = call_user_func_array(array($this->mainmodel,$method), $args);
			if( !is_array($result) ) $result = array();
			$data = array_merge($data, $result);
		}
		$args['data'] = $data;
		if(method_exists($this, $method)) {
			if( $method==='index' ) array_unshift($args, $method);
			call_user_func_array(array($this,$method), $args);
        }else{
			$subpage = $method;//$this->CI()->uri->segment(2, "index");
			array_unshift($args, $method);
			$method = "index";
			if(method_exists($this, $method)) {
				call_user_func_array(array($this,$method), $args);
			}
		}
		#	end create real contents

		#	create header
		$this->CI()->print_including('footer', "{$classname}.{$method}");
		#	create tail
		$this->CI()->print_including('tail', "{$classname}.{$method}");
	}
```

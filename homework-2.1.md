// This code is from Platform forked PHP file in ripository //


$user_id = false;
 if we've got a username we need to find the id — over-write no matter what. no fallback to user id 1

// a boolean with comment below//

	if ($user_request->response['payload']) {
			$user_id = $user_request->response['payload'];
		} else {
			$user_id = false;
			
// another boolean accompanied at top by the contstruc if //

if ($user_id) {
	$settings_request = new CASHRequest(
		array(
			'cash_request_type' => 'system',
			'cash_action' => 'getsettings',
			'type' => 'public_profile_template',
			'user_id' => $user_id
			
// The use of an Array//

	$template = false;
	if ($template_id) {
		$template_request = new CASHRequest(
			array(
				'cash_request_type' => 'system',
				'cash_action' => 'gettemplate',
				'template_id' => $template_id,
				'user_id' => $user_id
				
// Another Array accompanied by the use of a Boolean and a construct "if"//

(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
		(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
		m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
		
// The above example seems to consist of some Comparison operators// 

//All examples pulled from file WORD PRESS: INDEX PHP located under FOLDER named Indexes//
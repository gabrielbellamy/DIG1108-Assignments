The CODE below is pulled from forked project PLATFORM CORE folder CASHdata.PHP file


		if (rand(1,100) <= 2) {
			$gc = new CASHDaemon();
		}
		r
		
public function sessionGet($key,$scope='persistent') {
		if ($scope == 'persistent') {
			$session_data = $this->getAllSessionData();
			if (isset($session_data['persistent'][(string)$key])) {
				return $session_data['persistent'][(string)$key];
			} else {
				return false;
			}
		} else {
			if (isset($GLOBALS['cashmusic_script_store'][(string)$key])) {
				return $GLOBALS['cashmusic_script_store'][(string)$key];
			} else {
				return false;
// garbage collection daemon. 2% chance of running. //

				
 * Removes the key/value entry for a specified key

	 */public function sessionClear($key,$scope='persistent') {
		if ($scope == 'persistent') {
			$session_data = $this->getAllSessionData();
			if (!$session_data['persistent']) {
				$this->resetSession();
			} else if (isset($session_data['persistent'][(string)$key])) {
				unset($session_data['persistent'][(string)$key]);
				$session_id = $this->getSessionID();
				$expiration = time() + $this->cash_session_timeout;
				$this->db->setData(
					'sessions',
					array(
						'expiration_date' => $expiration,
						'data' => json_encode($session_data['persistent'])
					),
					array(
						'session_id' => array(
							'condition' => '=',
							'value' => $session_id
						)
					)
				);
			}
		} else {
			if (isset($GLOBALS['cashmusic_script_store'][(string)$key])) {
				unset($GLOBALS['cashmusic_script_store'][(string)$key]);				
		
// * Removes the key/value entry for a specified key //
		
	 */public function sessionClearAll() {
		$this->resetSession();
		// set the client-side cookie
		if (!headers_sent()) {
			// if headers have already been sent the cookie will be cleared on
			// next sessionStart()
			if (isset($_COOKIE['cashmusic_session'])) {
				setcookie('cashmusic_session', null, -1, '/');
			}
		}
// Reset the session in the database, expire the cookie //


	public function setMetaData($scope_table_alias,$scope_table_id,$user_id,$data_key,$data_value) {
		// try to find an exact key/value match
		$selected_tag = $this->getMetaData($scope_table_alias,$scope_table_id,$user_id,$data_key,$data_value);
		if (!$selected_tag) {
			$data_key_exists = $this->getMetaData($scope_table_alias,$scope_table_id,$user_id,$data_key);
			if ($data_key == 'tag' || !$data_key_exists) {
				// no matching tag or key, so we can just create a new one
				$result = $this->db->setData(
					'metadata',
					array(
						'scope_table_alias' => $scope_table_alias,
						'scope_table_id' => $scope_table_id,
						'type' => $data_key,
						'value' => $data_value,
						'user_id' => $user_id
					)
				);
			} else {
				// key already exists and isn't a tag, so we need to edit the value
				$result = $this->db->setData(
					'metadata',
					array(
						'value' => $data_value
					),
					array(
						'id' => array(
							'condition' => '=',
							'value' => $data_key_exists['id']
						)
					)
				);
			}
			return $result;
		} else {
		
// exact match: metadata exists as requested. return true // Metadata can be applied to any table by way of a scope table (alias) and
id. These functions make access available to all plants ....return true //
			
			
public function removeAllMetaData($scope_table_alias,$scope_table_id,$user_id=false,$ignore_or_match='match',$data_key=false) {
	
		$conditions_array = array(
			'scope_table_alias' => array(
				'condition' => '=',
				'value' => $scope_table_alias
			),
			'scope_table_id' => array(
				'condition' => '=',
				'value' => $scope_table_id
			)
		);
		if ($user_id) {
			// if a $user_id is present refine the search
			$conditions_array['user_id'] = array(
				'condition' => '=',
				'value' => $user_id
			);
		}
		if ($data_key) {
			$key_condition = "=";
			if ($ignore_or_match = 'ignore') {
				$key_condition = "!=";
			}
			$conditions_array['type'] = array(
				"condition" => $key_condition,
				"value" => $data_key
			);
		}
		$result = $this->db->deleteData(
			'metadata',
			$conditions_array
		);
		return $result;
		
// set table / id up front. if no user is specified it will remove ALL // metadata for a given table+id — used primarily when deleting the parent item //
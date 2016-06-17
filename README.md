370                 throw new CDbException('CDbConnection.connectionString cannot be empty.');
371             try
372             {
373                 Yii::trace('Opening DB connection','system.db.CDbConnection');
374                 $this->_pdo=$this->createPdoInstance();
375                 $this->initConnection($this->_pdo);
376                 $this->_active=true;
377             }
378             catch(PDOException $e)
379             {
380                 if(YII_DEBUG)
381                 {
382                     throw new CDbException('CDbConnection failed to open the DB connection: '.
383                         $e->getMessage(),(int)$e->getCode(),$e->errorInfo);
384                 }
385                 else
386                 {
387                     Yii::log($e->getMessage(),CLogger::LEVEL_ERROR,'exception.CDbException');
388                     throw new CDbException('CDbConnection failed to open the DB connection.',(int)$e->getCode(),$e->errorInfo);
389                 }
390             }
391         }
392     }
393 
394     /**
Stack Trace
#0	
+  /home/www/yii1113/db/CDbConnection.php(330): CDbConnection->open()
#1	
+  /home/www/yii1113/db/CDbConnection.php(308): CDbConnection->setActive(true)
#2	
+  /home/www/yii1113/base/CModule.php(387): CDbConnection->init()
#3	
+  /home/www/yii1113/base/CApplication.php(450): CModule->getComponent("db")
#4	
+  /home/www/yii1113/db/ar/CActiveRecord.php(634): CApplication->getDb()
#5	
+  /home/www/yii1113/db/ar/CActiveRecord.php(667): CActiveRecord->getDbConnection()
#6	
+  /home/www/yii1113/db/ar/CActiveRecord.php(1455): CActiveRecord->getCommandBuilder()
#7	
–  /home/www/protected-www/components/UserIdentity.php(35): CActiveRecord->find(CDbCriteria)
30 
31               $criteria = new CDbCriteria;
32               $criteria->select = 'id_user, salt, password';
33               $criteria->condition = 'LOWER(email)=:email';
34               $criteria->params = array(':email'=>$username);
35               $user = User::model()->find($criteria);
36 
37               $criteria2 = new CDbCriteria;
38               $criteria2->select = 'id_user';
39               $criteria2->condition = 'LOWER(email)=:email AND is_email_verified=:is_email_verified';
40               $criteria2->params = array(':email'=>$username, ':is_email_verified' => 1);
#8	
–  /home/www/protected-www/models/LoginForm.php(54): UserIdentity->authenticate()
49     public function authenticate($attribute,$params)
50     {
51         if(!$this->hasErrors())
52         {
53             $this->_identity=new UserIdentity($this->username,$this->password);
54             if(!$this->_identity->authenticate())
55             {
56                 if($this->_identity->errorCode === UserIdentity::ERROR_USERNAME_INACTIVE)
57                             $this->addError('password','Anda belum terverifikasi, silakan verifikasi melalui email anda');
58                 else
59                     $this->addError('password','Incorrect username or password.');
#9	
+  /home/www/yii1113/validators/CInlineValidator.php(42): LoginForm->authenticate("password", array())
#10	
+  /home/www/yii1113/validators/CValidator.php(213): CInlineValidator->validateAttribute(LoginForm, "password")
#11	
+  /home/www/yii1113/base/CModel.php(159): CValidator->validate(LoginForm, null)
#12	
–  /home/www/protected-www/controllers/SiteController.php(166): CModel->validate()
161 
162         // collect user input data
163         if (isset($_POST['LoginForm'])) {
164             $model->attributes = $_POST['LoginForm'];
165             // validate user input and redirect to the previous page if valid
166             if ($model->validate() && $model->login()) {
167                 $this->redirect(Yii::app()->homeUrl . '/profilUser');
168             }
169         }
170         // display the login form
171         //if(date('Y-m-d') > date('2015-04-27') && date('Y-m-d H:i:s') < date('2015-05-04 11:59:59'))
#13	
+  /home/www/protected-www/controllers/SiteController.php(30): SiteController->actionLogin()
#14	
+  /home/www/yii1113/web/actions/CInlineAction.php(49): SiteController->actionIndex()
#15	
+  /home/www/yii1113/web/CController.php(308): CInlineAction->runWithParams(array())
#16	
+  /home/www/yii1113/web/CController.php(286): CController->runAction(CInlineAction)
#17	
+  /home/www/yii1113/web/CController.php(265): CController->runActionWithFilters(CInlineAction, array())
#18	
+  /home/www/yii1113/web/CWebApplication.php(282): CController->run("")
#19	
+  /home/www/yii1113/web/CWebApplication.php(141): CWebApplication->runController("")
#20	
+  /home/www/yii1113/base/CApplication.php(180): CWebApplication->processRequest()
#21	
+  /home/www/beasiswa-dev/index.php(49): CApplication->run()

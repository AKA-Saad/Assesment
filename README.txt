Sorry I don't have much time to do detailed refactoring as well as unit testing. It is brief refactoring to tell you my idea about code 

Thank You

Refactor Needed:

1. Use Guzzle Instead of cURL function for API's.
2. Try catch proper handling for API's request.
3. Avoid hard coded url for API. 
4. Avoid too much commited code. 
5. Naming convention was not that good. Each variable and method explicitly tells their purpose.
6. Some methods are very lengthy. Break them into smaller functions which will be essential for another person to read your code.
7. Use appropriate techniques,  don't use logics which are lengthy and complex
   For example: 
   Bad:
     if ($time < 60) {
            return $time . 'min';
        } else if ($time == 60) {
            return '1h';
        }

        $hours = floor($time / 60);
        $minutes = ($time % 60);


    Good:
        $hours = floor($time / 60);
        $minutes = ($time -   floor($time / 60) * 60);
        return sprintf($format, $hours, $minutes);


        Both are performing same functionality but, my code is much simple and short.

8. Too much redundent data. Avoid redundency. And make common function for all redundent data.

For example:
In your code everywhere use mailer function with redundent functionality

Make a common function for all mails it will save your time and complexity.

    public function sendmail( $user , $job , $subject, $email , $verb ,  $text = '' , $session_time= '') //Method to save from redundency
    {
        $data = [
            'user'         => $user,
            'job'          => $job,
            'session_time' => $session_time,
            'for_text'     => $text
        ];
        $this->mailer->send($email, $user->name, $subject,  $verb , $data);

    }


9. Put all DB related logic into Eloquent models.
10. Code has no validation. Further more move validation from controllers to Request classes
11. A controller must have only one responsibility, so move business logic from controllers to service classes.That is big drawback of your code
12. there was no Mass assignment is your code.
13. Chunk data for data-heavy tasks. If your data is ver heavy please use chunk method like"
$this->chunk(500, function ($users) {
    foreach ($users as $user) {
        ...
    }
});

14. Prefer descriptive method and variable names over comments
15. Use config and language files, constants instead of text in the code
16. Please follow Follow Laravel naming conventions.
17. Kindly use smart laravel methods

For exmple in your code :

Bad:
->orderBy('due', 'desc')
Good:
->latest('due')

18. Pluck() automatically pluck certain column value within all rows into Array. You don't have to specify all();
19. With first() method you don't have to specify get()->first() instead just use ->first()
19. In constraint don't use common lines 

For Example:
Bad
if($condition)
{
    $flag='true';
    $str = 'common code';

}else{
      $flag='false';
    $str = 'common code';
}

Good
if($condition)
{
    $flag='true';
}else{
      $flag='false';
}
   $str = 'common code';

20. Avoid using ->where('column', '=', 1) condition instead use ->where('column', 1);
21. Keep your code simple and short
/ * Bad * /
if($codition)
{
    $flag= true;
}   
else{
    $flag = false;
}


 * Good * 
 $flag= $condition ? true : false ;

 22. Don't send unnecessary parameters to any method
 For Exapmle:

Bad

$this->function($request->all() , $request->id , $request->name);

Good

$this->function($request->all());

22. you used Carbon::now(), Carbon::today() instead use now(), today() ;

23. Do not get data from the .env file directly
Pass the data to config files instead and then use the config() helper function to use the data in an application.

24. use smart built in PHP or Laravel techniques instead of your lengthy and complex methods 

Bad: 
        $data = array();            // save job's information to data for sending Push
        $data['job_id'] = $job->id;
        $data['from_language_id'] = $job->from_language_id;
        $data['immediate'] = $job->immediate;
        $data['duration'] = $job->duration;
        $data['status'] = $job->status;
        $data['gender'] = $job->gender;
        $data['certified'] = $job->certified;
        $data['due'] = $job->due;
        $data['job_type'] = $job->job_type;
        $data['customer_phone_type'] = $job->customer_phone_type;
        $data['customer_physical_type'] = $job->customer_physical_type;
        $data['customer_town'] = $job->town;
        $data['customer_type'] = $job->user->userMeta->customer_type;

Good: 
  $data = json_decode(json_encode($job), true);  // It will automatically generate associate array.      

  25. Dependency injection in your code is good. 
  26. Try to write clean code 
  27. Use modern PHP syntax where possible, but don't forget about readability. 


Sorry I don't have time to do detailed refactoring as well as unit testing. It is brief refactoring to tell you my idea about code thanks


Thank you!



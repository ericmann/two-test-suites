##  Core Framework: Example

<pre><code lang="php">/**
 * Make sure new authors are created in WordPress
 */
public function test_checkauthor() {
  $command = new Importer();
                      
  // First author
  $mary_id = $command->checkauthor( 'maryshelley' );
  $mary = \get_user_by( 'id', $mary_id );
  $this->assertEquals( 'maryshelley', $mary->user_login );
                      
  // Second author
  $jane_id = $command->checkauthor( 'janeausten' );
  $this->assertNotEquals( $mary_id, $jane_id );
                      
  // Repeat first
  $mary_redux = $command->checkauthor( 'maryshelley' );
  $this->assertEquals( $mary_id, $mary_redux );
}</code></pre>

note:
    We test our `checkauthor()` function by requesting authors that should be in the database. If a user doesn't exist, a new entry is created. We want to verify _new_ entries are created each time and are unique. We'll test against a _real_ WordPress database.

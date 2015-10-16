##  WP_Mock: Example

<pre><code lang="php">/**
 * Make sure new authors are created in WordPress
 */
public function test_checkauthor() {
  \WP_Mock::wpFunction( 'wp_generate_password', array(
    'times'  => 3,
    'return' => 'password',
  ) );
  
  \WP_Mock::wpFunction( 'wp_create_user', array(
    'times'           => 2,
    'return_in_order' => array( 1, 2 ),
  ) );

  $command = new Importer();
                      
  // First author
  $mary_id = $command->checkauthor( 'maryshelley' );
  $this->assertEquals( 1, $mary_id );
                      
  // Second author
  $jane_id = $command->checkauthor( 'janeausten' );
  $this->assertNotEquals( $mary_id, $jane_id );
                      
  // Repeat first
  $mary_redux = $command->checkauthor( 'maryshelley' );
  $this->assertEquals( $mary_id, $mary_redux );
}</code></pre>

note:
    We test the same function as before, but this time we use WP_Mock to _mock_ WordPress' API. There is no `wp_generate_password()` or `wp_create_user()` function, so we have to program the implementations.

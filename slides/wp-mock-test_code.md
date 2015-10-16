##  WP_Mock: Example

<pre><code lang="php">class Importer {
  /**
   * @var Array Mapping of MT usernames to WordPress user IDs
   */
  private $mtnames = array();
                      
  /**
   * Check that the author exists within WordPress and, if not, create it.
   *
   * @param String $author
   *
   * @return int|\WP_Error
   */
  public function checkauthor( $author ) {
    $pass = wp_generate_password();
    if ( ! isset( $this->mtnames[ $author ] ) ) {
      $user_id = wp_create_user( $author, $pass );
      $this->mtnames[ $author ] = $user_id;
    } else {
      $user_id = $this->mtnames[ $author ];
    }
                      
    return $user_id;
  }
}</code></pre>

note:
    For comparison's sake, we're going to use the same code as before. This way, we compare apples to apples when viewing the two different test paradigms.

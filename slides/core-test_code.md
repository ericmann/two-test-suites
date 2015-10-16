##  Core Framework: Example

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
    Our test code comes from a MovableType importer. Our object needs to test incoming author names against existing WordPress objects. First things first, it tests to see if we already know of an author - if so, we return the existing ID and move along. If not, we create a new WordPress user, store their ID for later, and return the new entry.

# WordPress Query Comprehensive Reference
```php
<?php
/**
* WordPress Query Comprehensive Reference
* Compiled by luetkemj - luetkemj.github.io
*
* CODEX:    https://developer.wordpress.org/reference/classes/wp_query/#parameters
* Source:   https://core.trac.wordpress.org/browser/tags/6.0/src/wp-includes/query.php
*/

$args = [

// Author Parameters - Show posts associated with certain author.
// https://developer.wordpress.org/reference/classes/wp_query/#author-parameters
  'author'          =>  '1,2,3,',   // (int | string) -  use author id or comma-separated list of IDs [use minus (-) to exclude authors by ID ex. 'author' => '-1,-2,-3,']
  'author_name'     =>  'cc',       // (string) - use 'user_nicename' (NOT name)
  'author__in'      =>  [2, 6],     // (array) - use author id.
  'author__not_in'  =>  [2, 6],     // (array) - use author id.


// Category Parameters - Show posts associated with certain categories.
// https://developer.wordpress.org/reference/classes/wp_query/#parameters
  'cat'                 =>  5,              // (int) - Display posts that have this category (and any children of that category), using category id.
  'cat'                 =>  '-12,-34,-56',  // (string) - Display all posts except those from a category by prefixing its id with a '-' (minus) sign.
  'category_name'       =>  'staff, news',  // (string) - Display posts that have these categories (and any children of that category), using category slug.
  'category_name'       =>  'staff+news',   // (string) - Display posts that have "all" of these categories, using category slug.
  'category__and'       =>  [2, 6],         // (array) - Display posts that are in multiple categories. This shows posts that are in both categories 2 and 6.
  'category__in'        =>  [2, 6],         // (array) - Display posts that have this category (not children of that category), using category id.
  'category__not_in'    =>  [2, 6],         // (array) - Display posts that DO NOT HAVE these categories (not children of that category), using category id.


// Tag Parameters - Show posts associated with certain tags.
// https://developer.wordpress.org/reference/classes/wp_query/#tag-parameters
  'tag'             =>  'cooking',          // (string) - use tag slug.
  'tag_id'          =>  5,                  // (int) - use tag id.
  'tag__and'        =>  [2, 6],             // (array) - use tag ids.
  'tag__in'         =>  [2, 6],             // (array) - use tag ids.
  'tag__not_in'     =>  [2, 6],             // (array) - use tag ids.
  'tag_slug__and'   =>  ['red', 'blue'],    // (array) - use tag slugs.
  'tag_slug__in'    =>  ['red', 'blue'],    // (array) - use tag slugs.


// Taxonomy Parameters - Show posts associated with certain taxonomy.
// https://developer.wordpress.org/reference/classes/wp_query/#taxonomy-parameters
// Important Note: tax_query takes an array of tax query arguments arrays (it takes an array of arrays)
// This construct allows you to query multiple taxonomies by using the relation parameter in the first (outer) array to describe the boolean relationship between the taxonomy queries.
  'tax_query'   =>  [       // (array) - use taxonomy parameters.
    'relation'  =>  'AND',  // (string) - The logical relationship between each inner taxonomy array when there is more than one. Possible values are 'AND', 'OR'. Do not use with a single inner taxonomy array. Default value is 'AND'.
    [
      'taxonomy'            =>  'color',            // (string) - Taxonomy.
      'field'               =>  'slug',             // (string) - Select taxonomy term by Possible values are 'term_id', 'name', 'slug' or 'term_taxonomy_id'. Default value is 'term_id'.
      'terms'               =>  ['red', 'blue'],    // (int/string/array) - Taxonomy term(s).
      'include_children'    =>  true,               // (bool) - Whether or not to include children for hierarchical taxonomies. Defaults to true.
      'operator'            =>  'IN'                // (string) - Operator to test. Possible values are 'IN', 'NOT IN', 'AND', 'EXISTS' and 'NOT EXISTS'. Default value is 'IN'.
    ],
    [
      'taxonomy'            =>  'actor',
      'field'               =>  'id',
      'terms'               =>  [103, 115, 206 ],
      'include_children'    =>  false,
      'operator'            =>  'NOT IN'
    ]
],


// Post & Page Parameters - Display content based on post and page parameters.
// https://developer.wordpress.org/reference/classes/wp_query/#post-page-parameters
  'p'                       =>  1,                      // (int) - use post id.
  'name'                    =>  'hello-world',          // (string) - use post slug.
  'title'                   =>  'Hello World',          // (string) - use post title.
  'page_id'                 =>  1,                      // (int) - use page id.
  'pagename'                =>  'sample-page',          // (string) - use page slug.
  'pagename'                =>  'contact_us/canada',    // (string) - Display child page using the slug of the parent and the child page, separated by a slash (e.g. 'parent_slug/child_slug')
  'post_name__in'           =>  'sample-post',          // (array) - use post slugs. Specify posts to retrieve.
  'post_parent'             =>  1,                      // (int) - use page id. Return just the child Pages. (Only works with heirachical post types.)
  'post_parent__in'         =>  [1,2,3],                // (array) - use post ids. Specify posts whose parent is in an array.
  'post_parent__not_in'     =>  [1,2,3],                // (array) - use post ids. Specify posts whose parent is not in an array.
  'post__in'                =>  [1,2,3],                // (array) - use post ids. Specify posts to retrieve. ATTENTION If you use sticky posts, they will be included (prepended!) in the posts you retrieve whether you want it or not. To suppress this behaviour use ignore_sticky_posts
  'post__not_in'            =>  [1,2,3],                // (array) - use post ids. Specify post NOT to retrieve.
  // NOTE: you cannot combine 'post__in' and 'post__not_in' in the same query


// Password Parameters - Show content based on post and page parameters. Remember that default post_type is only set to display posts but not pages.
// https://developer.wordpress.org/reference/classes/wp_query/#password-parameters
  'has_password'    =>   true,          // (bool) - true for posts with passwords - false for posts without passwords - NULL for all posts with and without passwords
  'post_password'   =>  'multi-pass',   // (string) - show posts with a particular password.


// Post Type Parameters - Show posts associated with certain type or status.
// https://developer.wordpress.org/reference/classes/wp_query/#post-type-parameters
  'post_type'   =>  [       // (string / array) - use post types. Retrieves posts by Post Types, default value is 'post';
    'post',                 // - a post.
    'page',                 // - a page.
    'revision',             // - a revision.
    'attachment',           // - an attachment. The default WP_Query sets 'post_status'=>'published', but atchments default to 'post_status'=>'inherit' so you'll need to set the status to 'inherit' or 'any'.
    'nav_menu_item',        // - a navigation menu item
    'my-custom-post-type',  // - Custom Post Types (e.g. movies)
  ],
  // NOTE: The 'any' keyword available to both post_type and post_status queries cannot be used within an array.
  'post_type'   =>  'any',  // - retrieves any type except revisions and types with 'exclude_from_search' set to true.


// Post Status Parameters - Show posts associated with certain type or status.
// https://developer.wordpress.org/reference/classes/wp_query/#status-parameters
    'post_status'   =>  [   // (string | array) - use post status. Retrieves posts by Post Status, default value i'publish'.
      'publish',            // - a published post or page.
      'pending',            // - post is pending review.
      'draft',              // - a post in draft status.
      'auto-draft',         // - a newly created post, with no content.
      'future',             // - a post to publish in the future.
      'private',            // - visible only to the author, administrators, and editors.
      'inherit',            // - a revision. see get_children.
      'trash',              // - post is in trashbin.
    ],
    // NOTE: The 'any' keyword available to both post_type and post_status queries cannot be used within an array.
    'post_status'   =>  'any',  // - retrieves any status except those from post types with 'exclude_from_search' set to true.


// Comment Paremters
// https://developer.wordpress.org/reference/classes/wp_query/#comment-parameters
    'comment_count'     =>  10,     // (int | array) The amount of comments your CPT has to have ( Search operator will do a '=' operation )
    'comment_count'     =>  [
      'value'       =>  10,         // (int) - The amount of comments your CPT has to have when comparing
      'compare'     =>  '=',        // (string) - The search operator. Possible values are '=', '!=', '>', '>=', '<', '<='. Default value is '='.
    ],

// Pagination Parameters
//https://developer.wordpress.org/reference/classes/wp_query/#pagination-parameters
    'posts_per_page'    =>  10,                     // (int) - number of post to show per page. Use 'posts_per_page' => -1 to show all posts.
                                                    // Note: if the query is in a feed, wordpress overwrites this parameter with the stored 'posts_per_rss' option. Treimpose the limit, try using the 'post_limits' filter, or filter 'pre_option_posts_per_rss' and return -1
    'nopaging'          =>  false,                  // (bool) - show all posts or use pagination. Default value is 'false', use paging.
    'paged'             =>  get_query_var('paged'), // (int) - number of page. Show the posts that would normally show up just on page X when usinthe "Older Entries" link.
                                                    // NOTE: Use get_query_var('page'); if you want your query to work in a Page template that you've set as your static front page. The query variable 'page' holds the pagenumber for a single paginated Post or Page that includes the <!--nextpage--> Quicktag in the post content.
    'nopaging'                  => false,           // (boolean) - show all posts or use pagination. Default value is 'false', use paging.
    'posts_per_archive_page'    => 10,              // (int) - number of posts to show per page - on archive pages only. Over-rides posts_per_page and showposts on pages where is_archive() or is_search() would be true.
    'offset'                    => 3,               // (int) - number of post to displace or pass over.
                                                    // Warning: Setting the offset parameter overrides/ignores the paged parameter and breaks pagination. for a workaround see: http://codex.wordpress.org/Making_Custom_Queries_using_Offset_and_Pagination
                                                    // The 'offset' parameter is ignored when 'posts_per_page'=>-1 (show all posts) is used.
    'paged'     =>  get_query_var('paged'),         // (int) - number of page. Show the posts that would normally show up just on page X when usinthe "Older Entries" link.
                                                    // NOTE: This whole paging thing gets tricky. Some links to help you out:
                                                    // https://developer.wordpress.org/reference/functions/next_posts_link/#comment-1297
                                                    // http://codex.wordpress.org/Pagination#Troubleshooting_Broken_Pagination
    'page'      =>  get_query_var('page'),          // (int) - number of page for a static front page. Show the posts that would normally show up just on page X of a Static Front Page.
                                                    // NOTE: The query variable 'page' holds the pagenumber for a single paginated Post or Page that includes the <!--nextpage--> Quicktag in the post content.
    'ignore_sticky_posts'   =>  false,               // (boolean) - ignore sticky posts or not 1, replaced caller_get_posts parameter). Default value is 0 - don't ignore sticky posts. Note: ignore/exclude sticky posts being included at the beginning of posts returned, but the sticky post will still be returned in the natural order of that list of posts returned.


// Order & Orderby Parameters - Sort retrieved posts.
// https://developer.wordpress.org/reference/classes/wp_query/#order-orderby-parameters
    'order'     =>  'DESC',     // (string | array) - Designates the ascending or descending order of the 'orderby' parameter. Default to 'DESC'.
                                // Possible Values:
                                // 'ASC' - ascending order from lowest to highest values (1, 2, 3; a, b, c).
                                // 'DESC' - descending order from highest to lowest values (3, 2, 1; c, b, a).
    'orderby'   =>  'date',     // (string | array) - Sort retrieved posts by parameter. Defaults to 'date'. One or more options can be passed. EX: 'orderby' => 'menu_order title'
                                // Possible Values:
                                // 'none' - No order.
                                // 'ID' - Order by post id. Note the capitalization.
                                // 'author' - Order by author. ('post_author' is also accepted.)
                                // 'title' - Order by title. ('post_title' is also accepted.)
                                // 'name' - Order by post name (post slug). ('post_name' is also accepted.)
                                // 'type' - Order by post type. ('post_type' is also accepted.)
                                // 'date' - Order by date. ('post_date' is also accepted.)
                                // 'modified' - Order by last modified date. ('post_modified' is also accepted.)
                                // 'parent' - Order by post/page parent id. ('post_parent' is also accepted.)
                                // 'rand' - Random order. You can also use 'RAND(x)' where 'x' is an integer seed value.
                                // 'comment_count' - Order by number of comment.
                                // 'relevance' - Order by search terms in the following order: First, whether the entire sentence is matched. Second, if all the search terms are within the titles. Third, if any of the search terms appear in the titles. And, fourth, if the full sentence appears in the contents.
                                // 'menu_order' - Order by Page Order. Used most often for Pages (Order field in the Edit Page Attributes box) and for Attachments (the integer fields in the Insert / Upload Media Gallery dialog), but could be used for any post type with distinct 'menu_order' values (they all default to 0).
                                // 'meta_value' - Note that a 'meta_key=keyname' must also be present in the query. Note also that the sorting will be alphabetical which is fine for strings (i.e. words), but can be unexpected for numbers (e.g. 1, 3, 34, 4, 56, 6, etc, rather than 1, 3, 4, 6, 34, 56 as you might naturally expect). Use 'meta_value_num' instead for numeric values.
                                // 'meta_type' if you want to cast the meta value as a specific type. Possible values are 'NUMERIC', 'BINARY',  'CHAR', 'DATE', 'DATETIME', 'DECIMAL', 'SIGNED', 'TIME', 'UNSIGNED', same as in '$meta_query'. When using 'meta_type' you can also use 'meta_value_*' accordingly. For example, when using DATETIME as 'meta_type' you can use 'meta_value_datetime' to define order structure.
                                // 'meta_value_num' - Order by numeric meta value. Also note that a 'meta_key=keyname' must also be present in the query. This value allows for numerical sorting as noted above in 'meta_value'.
                                // 'post__in' - Preserve post ID order given in the 'post__in' array. Note - the value of the order parameter does not change the resulting sort order.
                                // 'post_name__in' - Preserve post slug order given in the 'post_name__in' array. Note - the value of the order parameter does not change the resulting sort order.
                                // 'post_parent__in' - Preserve post parent order given in the 'post_parent__in' array. Note - the value of the order parameter does not change the resulting sort order.

                                
// Date Parameters - Show posts associated with a certain time and date period.
// https://developer.wordpress.org/reference/classes/wp_query/#date-parameters
    'year'          =>  2014,       // (int) - 4 digit year (e.g. 2011).
    'monthnum'      =>  4,          // (int) - Month number (from 1 to 12).
    'w'             =>  25,         // (int) - Week of the year (from 0 to 53). Uses the MySQL WEEK command. The mode is dependenon the "start_of_week" option.
    'day'           =>  7,          // (int) - Day of the month (from 1 to 31).
    'hour'          =>  13,         // (int) - Hour (from 0 to 23).
    'minute'        =>  19,         // (int) - Minute (from 0 to 60).
    'second'        =>  30,         // (int) - Second (0 to 60).
    'm'             =>  201404,     // (int) - YearMonth (For e.g.: 201307).
    'date_query'    =>  [           // (array) - Date parameters.
        [
            'year'      =>  2014,                   // (int) - 4 digit year (e.g. 2011).
            'month'     =>  4,                      // (int) - Month number (from 1 to 12).
            'week'      =>  31,                     // (int) - Week of the year (from 0 to 53).
            'day'       =>  5,                      // (int) - Day of the month (from 1 to 31).
            'hour'      =>  2,                      // (int) - Hour (from 0 to 23).
            'minute'    =>  3,                      // (int) - Minute (from 0 to 59).
            'second'    =>  36,                     // (int) - Second (0 to 59).
            'after'     =>  'January 1st, 2013',    // (string/array) - Date to retrieve posts after. Accepts strtotime()-compatible string, or array of 'year', 'month', 'day'
            'before'    =>  [                       // (string/array) - Date to retrieve posts after. Accepts strtotime()-compatible string, or array of 'year', 'month', 'day'
                'year'      =>  2013,               // (string) Accepts any four-digit year. Default is empty.
                'month'     =>  2,                  // (string) The month of the year. Accepts numbers 1-12. Default: 12.
                'day'       =>  28,                 // (string) The day of the month. Accepts numbers 1-31. Default: last day of month.
            ],
            'inclusive' =>  true,           // (boolean) - For after/before, whether exact value should be matched or not'.
            'compare'   =>  '=',            // (string) - Possible values are '=', '!=', '>', '>=', '<', '<=', 'LIKE', 'NOT LIKE', 'IN', 'NOT IN', 'BETWEEN', 'NOT BETWEEN', 'EXISTS', and 'NOT EXISTS'. Default value is '='
            'column'    =>  'post_date',    // (string) - Column to query against. Default: 'post_date'.
            'relation'  =>  'AND',          // (string) - OR or AND, how the sub-arrays should be compared. Default: AND.
        ],
    ],

// Custom Field Parameters - Show posts associated with a certain custom field.
// https://developer.wordpress.org/reference/classes/wp_query/#custom-field-post-meta-parameters
    'meta_key'          =>  'key',      // (string) - Custom field key.
    'meta_value'        =>  'value',    // (string) - Custom field value.
    'meta_value_num'    =>  10,         // (number) - Custom field value.
    'meta_compare'      =>  '=',        // (string) - Operator to test. Possible values are '=', '!=', '>', '>=', '<', '<=', 'LIKE', 'NOT LIKE', 'IN', 'NOT IN', 'BETWEEN', 'NOT BETWEEN', 'EXISTS' and 'NOT EXISTS'. Default value is '='.
    'meta_query'        =>  [           // (array) - Custom field parameters.
        'relation'      =>  'AND',      // (string) - Possible values are 'AND', 'OR'. The logical relationship between each inner meta_query array when there is more than one. Do not use with a single inner meta_query array.
        [
         'key'      =>  'color',        // (string) - Custom field key.
         'value'    =>  'blue',         // (string/array) - Custom field value (Note: Array support is limited to a compare value of 'IN', 'NOT IN', 'BETWEEN', or 'NOT BETWEEN').
         'type'     =>  'CHAR',         // (string) - Custom field type. Possible values are 'NUMERIC', 'BINARY', 'CHAR', 'DATE', 'DATETIME', 'DECIMAL', 'SIGNED', 'TIME', 'UNSIGNED'. Default value is 'CHAR'.
                                        // NOTE: The 'type' DATE works with the 'compare' value BETWEEN only if the date is stored at the format YYYYMMDD and tested with this format.
         'compare'  =>  '=',            // (string) - Operator to test. Possible values are '=', '!=', '>', '>=', '<', '<=', 'LIKE', 'NOT LIKE', 'IN', 'NOT IN', 'BETWEEN', 'NOT BETWEEN', 'EXISTS', and 'NOT EXISTS'. Default value is '='.
        ],
        [
         'key'      =>  'price',
         'value'    =>  [1,200],
         'compare'  =>  'NOT LIKE',
        ]
    ],


// Permission Parameters - Display published posts, as well as private posts, if the user has the appropriate capability:
// https://developer.wordpress.org/reference/classes/wp_query/#permission-parameters
    'perm'  =>  'readable',     // (string) Possible values are 'readable', 'editable'

// Mime Type Parameters - Used with the attachments post type.
// https://developer.wordpress.org/reference/classes/wp_query/#mime-type-parameters
    'post_mime_type'    =>  'image/gif', // (string/array) - Allowed mime types.


// Caching Parameters
// https://developer.wordpress.org/reference/classes/wp_query/#caching-parameters
// NOTE Caching is a good thing. Setting these to false is generally not advised.
    'cache_results'             =>  true,   // (bool) Default is true - Post information cache.
    'update_post_term_cache'    =>  true,   // (bool) Default is true - Post term information cache.
    'update_post_meta_cache'    =>  true,   // (bool) Default is true - Post meta information cache.
    'no_found_rows'             =>  false,  // (bool) Default is false. WordPress uses SQL_CALC_FOUND_ROWS in most queries in order to implement pagination. Even when you don't need pagination at all. By Setting this parameter to true you are telling wordPress not to count the total rows and reducing load on the DB. Pagination will NOT WORK when this parameter is set to true. For more information see: http://flavio.tordini.org/speed-up-wordpress-get_posts-and-query_posts-functions


// Search Parameter
// https://developer.wordpress.org/reference/classes/wp_query/#search-parameters
    's'             =>  $s, // (string) - Passes along the query string variable from a search. For example usage see: http://www.wprecipes.com/how-to-display-the-number-of-results-in-wordpress-search
    'exact'         =>  true, // (bool) - flag to make it only match whole titles/posts - Default value is false. For more information see: https://gist.github.com/2023628#gistcomment-285118
    'sentence'      =>  true, // (bool) - flag to make it do a phrase search - Default value is false. For more information see: https://gist.github.com/2023628#gistcomment-285118

// Post Field Parameters
// https://developer.wordpress.org/reference/classes/wp_query/#return-fields-parameter
// also https://gist.github.com/luetkemj/2023628/#comment-1003542
    'fields'    =>  'ids',  // (string) - Which fields to return. All fields are returned by default.
                            // Possible values:
                            // 'ids'        - Return an array of post IDs.
                            // 'id=>parent' - Return an associative array [ parent => ID, … ].
                            // Passing anything else will return all fields (default) - an array of post objects.


];

$the_query = new WP_Query( $args );

// The Loop
if ($the_query->have_posts()) {
    while ($the_query->have_posts()) {
        $the_query->the_post();
        // Do Stuff
    }
}

// Reset Post Data
wp_reset_postdata();

// Reset query - if you need to run a second query from the same function
wp_reset_query();

?>
```

## Contributing

Contributions are welcome.

Find a problem? Open an [issue](https://github.com/luetkemj/wp-query-ref/issues)!

Better yet, fix it yourself and open a pull request!

Never submitted a pull request before? You can learn how from this free series [How to Contribute to an Open Source Project on GitHub](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github)

# php-md5-streamfilter

A simple stream filter to calculate the MD5 hash of a PHP stream. Attach the
filter to the stream, process the stream, and when you're done, call
`md5s_get_hash()` to fetch the hash.

## License

This code is licensed under the [New BSD
license](http://opensource.org/licenses/BSD-3-Clause). The same code can also
be found in the Webfolders package, where it is licensed under the GNU Affero
GPL version 3.

## Usage example

    require_once 'streamfilter.md5.php';

    // Setup code, acquire a stream in $fd:
    $fd = fopen('test.txt');

    // Register stream filter, append to filter chain:
    stream_filter_register('md5sum', 'md5sum_filter');
    $md5_filter = stream_filter_append($fd, 'md5sum');

    // Dummy file read, just to get the data flowing;
    // in reality this might be a stream_copy_to_stream() invocation:
    while (fread($fd, 5000000));

    // Remove filter, close handle, print hash:
    stream_filter_remove($md5_filter);
    close($fd);
    echo "MD5: " . md5s_get_hash();

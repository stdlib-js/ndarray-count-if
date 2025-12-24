<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# countIf

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Count the number of truthy elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions.

<section class="intro">

</section>

<!-- /.intro -->



<section class="usage">

## Usage

```javascript
import countIf from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-count-if@esm/index.mjs';
```

You can also import the following named exports from the package:

```javascript
import { assign } from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-count-if@esm/index.mjs';
```

#### countIf( x\[, options], predicate\[, thisArg] )

Counts the number of truthy elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';

function clbk( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Perform reduction:
var out = countIf( x, clbk );
// returns <ndarray>[ 5 ]
```

The function accepts the following arguments:

-   **x**: input [`ndarray`][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context (_optional_).

The function accepts the following `options`:

-   **dims**: list of dimensions over which to perform a reduction.
-   **keepdims**: boolean indicating whether the reduced dimensions should be included in the returned [`ndarray`][@stdlib/ndarray/ctor] as singleton dimensions. Default: `false`.

By default, the function performs a reduction over all elements in a provided [`ndarray`][@stdlib/ndarray/ctor]. To reduce specific dimensions, set the `dims` option.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';

function clbk( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Perform reduction:
var opts = {
    'dims': [ 1, 2 ]
};
var out = countIf( x, opts, clbk );
// returns <ndarray>[ 2, 2, 1 ]
```

By default, the function returns an [`ndarray`][@stdlib/ndarray/ctor] having a shape matching only the non-reduced dimensions of the input [`ndarray`][@stdlib/ndarray/ctor] (i.e., the reduced dimensions are dropped). To include the reduced dimensions as singleton dimensions in the output [`ndarray`][@stdlib/ndarray/ctor], set the `keepdims` option to `true`.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';

function clbk( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Perform reduction:
var opts = {
    'dims': [ 1, 2 ],
    'keepdims': true
};
var out = countIf( x, opts, clbk );
// returns <ndarray>[ [ [ 2 ] ], [ [ 2 ] ], [ [ 1 ] ] ]
```

To set the predicate function execution context, provide a `thisArg`.

<!-- eslint-disable no-invalid-this -->

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';

function clbk( value ) {
    this.count += 1;
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Create a context object:
var ctx = {
    'count': 0
};

// Perform reduction:
var out = countIf( x, clbk, ctx );
// returns <ndarray>[ 5 ]

var count = ctx.count;
// returns 6
```

#### countIf.assign( x, out\[, options], predicate\[, thisArg] )

Counts the number of truthy elements along one or more [`ndarray`][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [`ndarray`][@stdlib/ndarray/ctor].

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';
import empty from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-empty@esm/index.mjs';

function clbk( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Create an output ndarray:
var y = empty( [], {
    'dtype': 'int32'
});

// Perform reduction:
var out = countIf.assign( x, y, clbk );
// returns <ndarray>[ 5 ]

var bool = ( out === y );
// returns true
```

The function accepts the following arguments:

-   **x**: input [`ndarray`][@stdlib/ndarray/ctor].
-   **out**: output [`ndarray`][@stdlib/ndarray/ctor]. The output [`ndarray`][@stdlib/ndarray/ctor] must have a shape matching the non-reduced dimensions of the input [`ndarray`][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context (_optional_).

The function accepts the following `options`:

-   **dims**: list of dimensions over which to perform a reduction.

By default, the function performs a reduction over all elements in a provided [`ndarray`][@stdlib/ndarray/ctor]. To reduce specific dimensions, set the `dims` option.

```javascript
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@esm/index.mjs';
import empty from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-empty@esm/index.mjs';

function clbk( value ) {
    return value > 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ] ], [ [ 3.0, 4.0 ] ], [ [ 0.0, 6.0 ] ] ] );
// returns <ndarray>

// Create an output ndarray:
var y = empty( [ 3 ], {
    'dtype': 'int32'
});

// Perform reduction:
var opts = {
    'dims': [ 1, 2 ]
};
var out = countIf.assign( x, y, opts, clbk );
// returns <ndarray>[ 2, 2, 1 ]

var bool = ( out === y );
// returns true
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The predicate function is provided the following arguments:

    -   **value**: current array element.
    -   **indices**: current array element indices.
    -   **arr**: the input ndarray.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="module">

var bernoulli = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/random-base-bernoulli' ).factory;
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@esm/index.mjs';
import fillBy from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-fill-by@esm/index.mjs';
import zeros from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-zeros@esm/index.mjs';
var isPositiveNumber = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/assert-is-positive-number' ).isPrimitive;
import countIf from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-count-if@esm/index.mjs';

var x = zeros( [ 2, 4, 5 ], {
    'dtype': 'float64'
});
x = fillBy( x, bernoulli( 0.90 ) );
console.log( ndarray2array( x ) );

var y = countIf( x, isPositiveNumber );
console.log( 'countIf(x[:,:,:]) =' );
console.log( y.get() );

var opts = {
    'dims': [ 0 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[:,j,k]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 1 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[i,:,k]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 2 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[i,j,:]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 0, 1 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[:,:,k]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 0, 2 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[:,j,:]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 1, 2 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[i,:,:]) =' );
console.log( ndarray2array( y ) );

opts = {
    'dims': [ 0, 1, 2 ],
    'keepdims': true
};
y = countIf( x, opts, isPositiveNumber );
console.log( 'countIf(x[:,:,:]) =' );
console.log( ndarray2array( y ) );

</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/ndarray-count-if.svg
[npm-url]: https://npmjs.org/package/@stdlib/ndarray-count-if

[test-image]: https://github.com/stdlib-js/ndarray-count-if/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/ndarray-count-if/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/ndarray-count-if/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/ndarray-count-if?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/ndarray-count-if.svg
[dependencies-url]: https://david-dm.org/stdlib-js/ndarray-count-if/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/ndarray-count-if/tree/deno
[deno-readme]: https://github.com/stdlib-js/ndarray-count-if/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/ndarray-count-if/tree/umd
[umd-readme]: https://github.com/stdlib-js/ndarray-count-if/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/ndarray-count-if/tree/esm
[esm-readme]: https://github.com/stdlib-js/ndarray-count-if/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/ndarray-count-if/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/ndarray-count-if/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/esm

<!-- <related-links> -->

<!-- </related-links> -->

</section>

<!-- /.links -->

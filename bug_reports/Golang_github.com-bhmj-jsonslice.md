Results do not match other implementations

The following queries provide results that do not match those of other implementations of JSONPath
(compare https://cburgmer.github.io/json-path-comparison/):

- [ ] `$['missing']`
  Input:
  ```
  {
    "key": "value"
  }
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$['ü']`
  Input:
  ```
  {
    "u\u0308": 42
  }
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[]`
  Input:
  ```
  {
    "": 42,
    "''": 123,
    "\"\"": 222
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  field not found
  ```

- [ ] `$['']`
  Input:
  ```
  {
    "": 42,
    "''": 123,
    "\"\"": 222
  }
  ```
  Expected output:
  ```
  42
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[""]`
  Input:
  ```
  {
    "": 42,
    "''": 123,
    "\"\"": 222
  }
  ```
  Expected output:
  ```
  42
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[-2]`
  Input:
  ```
  [
    "one element"
  ]
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[-1]`
  Input:
  ```
  []
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[0]`
  Input:
  ```
  {
    "0": "value"
  }
  ```
  Expected output:
  ```
  null
  ```
  Actual output:
  ```
  "value"
  ```

- [ ] `$[1]`
  Input:
  ```
  [
    "one element"
  ]
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$[0]`
  Input:
  ```
  "Hello World"
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$['\\']`
  Input:
  ```
  {
    "\\": "value"
  }
  ```
  Error:
  ```
  path: unexpected end of path at 7
  ```

- [ ] `$[':@."$,*\'\\']`
  Input:
  ```
  {
    ":@.\"$,*'\\": 42
  }
  ```
  Error:
  ```
  path: unexpected end of path at 16
  ```

- [ ] `$['single'quote']`
  Input:
  ```
  {
    "single'quote": "value"
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 10
  ```

- [ ] `$['*']`
  Input:
  ```
  {
    "another": "entry"
  }
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$['two'.'some']`
  Input:
  ```
  {
    "one": {
      "key": "value"
    },
    "two": {
      "some": "more",
      "key": "other value"
    },
    "two.some": "42",
    "two'.'some": "43"
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 7
  ```

- [ ] `$[two.some]`
  Input:
  ```
  {
    "one": {
      "key": "value"
    },
    "two": {
      "some": "more",
      "key": "other value"
    },
    "two.some": "42"
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 5
  ```

- [ ] `$[0:2][*]`
  Input:
  ```
  [
    [
      1,
      2
    ],
    [
      "a",
      "b"
    ],
    [
      0,
      0
    ]
  ]
  ```
  Expected output:
  ```
  [1, 2, "a", "b"]
  ```
  Actual output:
  ```
  [
    [
      1,
      2
    ],
    [
      "a",
      "b"
    ]
  ]
  ```

- [ ] `$[*].bar[*]`
  Input:
  ```
  [
    {
      "bar": [
        42
      ]
    }
  ]
  ```
  Expected output:
  ```
  [42]
  ```
  Actual output:
  ```
  [
    [
      42
    ]
  ]
  ```

- [ ] `$..[*]`
  Input:
  ```
  {
    "key": "value",
    "another key": {
      "complex": "string",
      "primitives": [
        0,
        1
      ]
    }
  }
  ```
  Expected output (in any order as no consensus on ordering exists):
  ```
  ["string", "value", 0, 1, [0, 1], {"complex": "string", "primitives": [0, 1]}]
  ```
  Actual output:
  ```
  [
    "value"
  ]
  ```

- [ ] `$[key]`
  Input:
  ```
  {
    "key": "value"
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Actual output:
  ```
  "value"
  ```

- [ ] `@.a`
  Input:
  ```
  {
    "a": 1
  }
  ```
  Error:
  ```
  path: $ expected
  ```

- [ ] `$.[key]`
  Input:
  ```
  {
    "key": "value",
    "other": {
      "key": [
        {
          "key": 42
        }
      ]
    }
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Actual output:
  ```
  "value"
  ```

- [ ] `$..[1].key`
  Input:
  ```
  {
    "k": [
      {
        "key": "some value"
      },
      {
        "key": 42
      }
    ],
    "kk": [
      [
        {
          "key": 100
        },
        {
          "key": 200
        },
        {
          "key": 300
        }
      ],
      [
        {
          "key": 400
        },
        {
          "key": 500
        },
        {
          "key": 600
        }
      ]
    ],
    "key": [
      0,
      1
    ]
  }
  ```
  Expected output (in any order as no consensus on ordering exists):
  ```
  [200, 42, 500]
  ```
  Actual output:
  ```
  [
    42
  ]
  ```

- [ ] `$.key`
  Input:
  ```
  [
    0,
    1
  ]
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$.id`
  Input:
  ```
  [
    {
      "id": 2
    }
  ]
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$.missing`
  Input:
  ```
  {
    "key": "value"
  }
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$.key-dash`
  Input:
  ```
  {
    "key-dash": "value"
  }
  ```
  Expected output:
  ```
  "value"
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$.`
  Input:
  ```
  {
    "key": 42,
    "": 9001,
    "''": "nice"
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: unexpected end of path at 2
  ```

- [ ] `$.length`
  Input:
  ```
  [
    4,
    5,
    6
  ]
  ```
  Expected output:
  ```
  null
  ```
  Error:
  ```
  No JSON output received
  ```

- [ ] `$.*.bar.*`
  Input:
  ```
  [
    {
      "bar": [
        42
      ]
    }
  ]
  ```
  Expected output:
  ```
  [42]
  ```
  Actual output:
  ```
  [
    [
      42
    ]
  ]
  ```

- [ ] `$a`
  Input:
  ```
  {
    "a": 1,
    "$a": 2
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 1
  ```

- [ ] `.key`
  Input:
  ```
  {
    "key": "value"
  }
  ```
  Error:
  ```
  path: $ expected
  ```

- [ ] `key`
  Input:
  ```
  {
    "key": "value"
  }
  ```
  Error:
  ```
  path: $ expected
  ```

- [ ] ``
  Input:
  ```
  {
    "a": 42,
    "": 21
  }
  ```
  Error:
  ```
  path: empty
  ```

- [ ] `$[?(@.key+50==100)]`
  Input:
  ```
  [
    {
      "key": 60
    },
    {
      "key": 50
    },
    {
      "key": 10
    },
    {
      "key": -50
    },
    {
      "key+50": 100
    }
  ]
  ```
  Error:
  ```
  invalid operands for arithmetic operator
  ```

- [ ] `$[?(@.key>0 && false)]`
  Input:
  ```
  [
    {
      "key": 1
    },
    {
      "key": 3
    },
    {
      "key": "nice"
    },
    {
      "key": true
    },
    {
      "key": null
    },
    {
      "key": false
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": -1
    },
    {
      "key": 0
    },
    {
      "key": ""
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key>0 && true)]`
  Input:
  ```
  [
    {
      "key": 1
    },
    {
      "key": 3
    },
    {
      "key": "nice"
    },
    {
      "key": true
    },
    {
      "key": null
    },
    {
      "key": false
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": -1
    },
    {
      "key": 0
    },
    {
      "key": ""
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key>0 || false)]`
  Input:
  ```
  [
    {
      "key": 1
    },
    {
      "key": 3
    },
    {
      "key": "nice"
    },
    {
      "key": true
    },
    {
      "key": null
    },
    {
      "key": false
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": -1
    },
    {
      "key": 0
    },
    {
      "key": ""
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key>0 || true)]`
  Input:
  ```
  [
    {
      "key": 1
    },
    {
      "key": 3
    },
    {
      "key": "nice"
    },
    {
      "key": true
    },
    {
      "key": null
    },
    {
      "key": false
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": -1
    },
    {
      "key": 0
    },
    {
      "key": ""
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@[-1]==2)]`
  Input:
  ```
  [
    [
      2,
      3
    ],
    [
      "a"
    ],
    [
      0,
      2
    ],
    [
      2
    ]
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.a && (@.b || @.c))]`
  Input:
  ```
  [
    {
      "a": true
    },
    {
      "a": true,
      "b": true
    },
    {
      "a": true,
      "b": true,
      "c": true
    },
    {
      "b": true,
      "c": true
    },
    {
      "a": true,
      "c": true
    },
    {
      "c": true
    },
    {
      "b": true
    }
  ]
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?(@.key/10==5)]`
  Input:
  ```
  [
    {
      "key": 60
    },
    {
      "key": 50
    },
    {
      "key": 10
    },
    {
      "key": -50
    },
    {
      "key/10": 5
    }
  ]
  ```
  Error:
  ```
  invalid operands for arithmetic operator
  ```

- [ ] `$[?(@.key-dash == 'value')]`
  Input:
  ```
  [
    {
      "key-dash": "value"
    }
  ]
  ```
  Error:
  ```
  unknown token at 10
  ```

- [ ] `$[?()]`
  Input:
  ```
  [
    1,
    {
      "key": 42
    },
    "value",
    null
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  empty filter
  ```

- [ ] `$[?(@.key==42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "some"
    },
    {
      "key": "42"
    },
    {
      "key": null
    },
    {
      "key": 420
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": [
        42
      ]
    },
    {
      "key": {
        "key": 42
      }
    },
    {
      "key": {
        "some": 42
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.d==["v1","v2"])]`
  Input:
  ```
  [
    {
      "d": [
        "v1",
        "v2"
      ]
    },
    {
      "d": [
        "a",
        "b"
      ]
    },
    {
      "d": "v1"
    },
    {
      "d": "v2"
    },
    {
      "d": {}
    },
    {
      "d": []
    },
    {
      "d": null
    },
    {
      "d": -1
    },
    {
      "d": 0
    },
    {
      "d": 1
    },
    {
      "d": "['v1','v2']"
    },
    {
      "d": "['v1', 'v2']"
    },
    {
      "d": "v1,v2"
    },
    {
      "d": "[\"v1\", \"v2\"]"
    },
    {
      "d": "[\"v1\",\"v2\"]"
    }
  ]
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?(@[0:1]==[1])]`
  Input:
  ```
  [
    [
      1,
      2,
      3
    ],
    [
      1
    ],
    [
      2,
      3
    ],
    1,
    2
  ]
  ```
  Error:
  ```
  unknown token at 12
  ```

- [ ] `$[?(@.*==[1,2])]`
  Input:
  ```
  [
    [
      1,
      2
    ],
    [
      2,
      3
    ],
    [
      1
    ],
    [
      2
    ],
    [
      1,
      2,
      3
    ],
    1,
    2,
    3
  ]
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?(@.d==['v1','v2'])]`
  Input:
  ```
  [
    {
      "d": [
        "v1",
        "v2"
      ]
    },
    {
      "d": [
        "a",
        "b"
      ]
    },
    {
      "d": "v1"
    },
    {
      "d": "v2"
    },
    {
      "d": {}
    },
    {
      "d": []
    },
    {
      "d": null
    },
    {
      "d": -1
    },
    {
      "d": 0
    },
    {
      "d": 1
    },
    {
      "d": "['v1','v2']"
    },
    {
      "d": "['v1', 'v2']"
    },
    {
      "d": "v1,v2"
    },
    {
      "d": "[\"v1\", \"v2\"]"
    },
    {
      "d": "[\"v1\",\"v2\"]"
    }
  ]
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?((@.key<44)==false)]`
  Input:
  ```
  [
    {
      "key": 42
    },
    {
      "key": 43
    },
    {
      "key": 44
    }
  ]
  ```
  Error:
  ```
  unknown token at 4
  ```

- [ ] `$[?(@.key==false)]`
  Input:
  ```
  [
    {
      "some": "some value"
    },
    {
      "key": true
    },
    {
      "key": false
    },
    {
      "key": null
    },
    {
      "key": "value"
    },
    {
      "key": ""
    },
    {
      "key": 0
    },
    {
      "key": 1
    },
    {
      "key": -1
    },
    {
      "key": 42
    },
    {
      "key": {}
    },
    {
      "key": []
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key==null)]`
  Input:
  ```
  [
    {
      "some": "some value"
    },
    {
      "key": true
    },
    {
      "key": false
    },
    {
      "key": null
    },
    {
      "key": "value"
    },
    {
      "key": ""
    },
    {
      "key": 0
    },
    {
      "key": 1
    },
    {
      "key": -1
    },
    {
      "key": 42
    },
    {
      "key": {}
    },
    {
      "key": []
    }
  ]
  ```
  Error:
  ```
  unknown token at 11
  ```

- [ ] `$[?(@[0:1]==1)]`
  Input:
  ```
  [
    [
      1,
      2,
      3
    ],
    [
      1
    ],
    [
      2,
      3
    ],
    1,
    2
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@[*]==2)]`
  Input:
  ```
  [
    [
      1,
      2
    ],
    [
      2,
      3
    ],
    [
      1
    ],
    [
      2
    ],
    [
      1,
      2,
      3
    ],
    1,
    2,
    3
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.*==2)]`
  Input:
  ```
  [
    [
      1,
      2
    ],
    [
      2,
      3
    ],
    [
      1
    ],
    [
      2
    ],
    [
      1,
      2,
      3
    ],
    1,
    2,
    3
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key==-0.123e2)]`
  Input:
  ```
  [
    {
      "key": -12.3
    },
    {
      "key": -0.123
    },
    {
      "key": -12
    },
    {
      "key": 12.3
    },
    {
      "key": 2
    },
    {
      "key": "-0.123e2"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key==010)]`
  Input:
  ```
  [
    {
      "key": "010"
    },
    {
      "key": "10"
    },
    {
      "key": 10
    },
    {
      "key": 0
    },
    {
      "key": 8
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.d=={"k":"v"})]`
  Input:
  ```
  [
    {
      "d": {
        "k": "v"
      }
    },
    {
      "d": {
        "a": "b"
      }
    },
    {
      "d": "k"
    },
    {
      "d": "v"
    },
    {
      "d": {}
    },
    {
      "d": []
    },
    {
      "d": null
    },
    {
      "d": -1
    },
    {
      "d": 0
    },
    {
      "d": 1
    },
    {
      "d": "[object Object]"
    },
    {
      "d": "{\"k\": \"v\"}"
    },
    {
      "d": "{\"k\":\"v\"}"
    },
    "v"
  ]
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?(@==42)]`
  Input:
  ```
  [
    0,
    42,
    -1,
    41,
    43,
    42.0001,
    41.9999,
    null,
    100
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key=="value")]`
  Input:
  ```
  [
    {
      "key": "some"
    },
    {
      "key": "value"
    },
    {
      "key": null
    },
    {
      "key": 0
    },
    {
      "key": 1
    },
    {
      "key": -1
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": "valuemore"
    },
    {
      "key": "morevalue"
    },
    {
      "key": [
        "value"
      ]
    },
    {
      "key": {
        "some": "value"
      }
    },
    {
      "key": {
        "key": "value"
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key==true)]`
  Input:
  ```
  [
    {
      "some": "some value"
    },
    {
      "key": true
    },
    {
      "key": false
    },
    {
      "key": null
    },
    {
      "key": "value"
    },
    {
      "key": ""
    },
    {
      "key": 0
    },
    {
      "key": 1
    },
    {
      "key": -1
    },
    {
      "key": 42
    },
    {
      "key": {}
    },
    {
      "key": []
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key>42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key>=42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.d in [2, 3])]`
  Input:
  ```
  [
    {
      "d": 1
    },
    {
      "d": 2
    },
    {
      "d": 1
    },
    {
      "d": 3
    },
    {
      "d": 4
    }
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Actual output:
  ```
  []
  ```

- [ ] `$[?(2 in @.d)]`
  Input:
  ```
  [
    {
      "d": [
        1,
        2,
        3
      ]
    },
    {
      "d": [
        2
      ]
    },
    {
      "d": [
        1
      ]
    },
    {
      "d": [
        3,
        4
      ]
    },
    {
      "d": [
        4,
        2
      ]
    }
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  unknown token at 5
  ```

- [ ] `$[?(@.key<42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key<=42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@.key*2==100)]`
  Input:
  ```
  [
    {
      "key": 60
    },
    {
      "key": 50
    },
    {
      "key": 10
    },
    {
      "key": -50
    },
    {
      "key*2": 100
    }
  ]
  ```
  Error:
  ```
  invalid operands for arithmetic operator
  ```

- [ ] `$[?(!(@.key==42))]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  unknown token at 4
  ```

- [ ] `$[?(!(@.key<42))]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "43"
    },
    {
      "key": "42"
    },
    {
      "key": "41"
    },
    {
      "key": "value"
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  unknown token at 4
  ```

- [ ] `$[?(@.key!=42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "some"
    },
    {
      "key": "42"
    },
    {
      "key": null
    },
    {
      "key": 420
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": [
        42
      ]
    },
    {
      "key": {
        "key": 42
      }
    },
    {
      "key": {
        "some": 42
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$[?(@[*]>=4)]`
  Input:
  ```
  [
    [
      1,
      2
    ],
    [
      3,
      4
    ],
    [
      5,
      6
    ]
  ]
  ```
  Error:
  ```
  operand types do not match
  ```

- [ ] `$.x[?(@[*]>=$.y[*])]`
  Input:
  ```
  {
    "x": [
      [
        1,
        2
      ],
      [
        3,
        4
      ],
      [
        5,
        6
      ]
    ],
    "y": [
      3,
      4,
      5
    ]
  }
  ```
  Error:
  ```
  operator is not applicable to strings
  ```

- [ ] `$[?(@.key=42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "some"
    },
    {
      "key": "42"
    },
    {
      "key": null
    },
    {
      "key": 420
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": [
        42
      ]
    },
    {
      "key": {
        "key": 42
      }
    },
    {
      "key": {
        "some": 42
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  unknown token at 9
  ```

- [ ] `$[?(@.key-50==-100)]`
  Input:
  ```
  [
    {
      "key": 60
    },
    {
      "key": 50
    },
    {
      "key": 10
    },
    {
      "key": -50
    },
    {
      "key-50": -100
    }
  ]
  ```
  Error:
  ```
  invalid operands for arithmetic operator
  ```

- [ ] `$[?(@.key===42)]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "some"
    },
    {
      "key": "42"
    },
    {
      "key": null
    },
    {
      "key": 420
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": [
        42
      ]
    },
    {
      "key": {
        "key": 42
      }
    },
    {
      "key": {
        "some": 42
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Error:
  ```
  unknown token at 11
  ```

- [ ] `$[?(null)]`
  Input:
  ```
  [
    1,
    3,
    "nice",
    true,
    null,
    false,
    {},
    [],
    -1,
    0,
    ""
  ]
  ```
  Error:
  ```
  unknown token at 4
  ```

- [ ] `$[?@.key==42]`
  Input:
  ```
  [
    {
      "key": 0
    },
    {
      "key": 42
    },
    {
      "key": -1
    },
    {
      "key": 1
    },
    {
      "key": 41
    },
    {
      "key": 43
    },
    {
      "key": 42.0001
    },
    {
      "key": 41.9999
    },
    {
      "key": 100
    },
    {
      "key": "some"
    },
    {
      "key": "42"
    },
    {
      "key": null
    },
    {
      "key": 420
    },
    {
      "key": ""
    },
    {
      "key": {}
    },
    {
      "key": []
    },
    {
      "key": [
        42
      ]
    },
    {
      "key": {
        "key": 42
      }
    },
    {
      "key": {
        "some": 42
      }
    },
    {
      "some": "value"
    }
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 4
  ```

- [ ] `$[?(!@.key)]`
  Input:
  ```
  [
    {
      "some": "some value"
    },
    {
      "key": true
    },
    {
      "key": false
    },
    {
      "key": null
    },
    {
      "key": "value"
    },
    {
      "key": ""
    },
    {
      "key": 0
    },
    {
      "key": 1
    },
    {
      "key": -1
    },
    {
      "key": 42
    },
    {
      "key": {}
    },
    {
      "key": []
    }
  ]
  ```
  Error:
  ```
  unknown token at 4
  ```

- [ ] `$.data.sum()`
  Input:
  ```
  {
    "data": [
      1,
      2,
      3,
      4
    ]
  }
  ```
  Error:
  ```
  path: unknown function at 10
  ```

- [ ] `$(key,more)`
  Input:
  ```
  {
    "key": 1,
    "some": 2,
    "more": 3
  }
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Error:
  ```
  path: invalid character at 1
  ```

- [ ] `$..`
  Input:
  ```
  [
    {
      "a": {
        "b": "c"
      }
    },
    [
      0,
      1
    ]
  ]
  ```
  Error:
  ```
  path: unexpected end of path at 3
  ```

- [ ] `$.key..`
  Input:
  ```
  {
    "some key": "value",
    "key": {
      "complex": "string",
      "primitives": [
        0,
        1
      ]
    }
  }
  ```
  Error:
  ```
  path: unexpected end of path at 7
  ```

- [ ] `$[(@.length-1)]`
  Input:
  ```
  [
    "first",
    "second",
    "third",
    "forth",
    "fifth"
  ]
  ```
  Error:
  ```
  path: invalid character at 2
  ```

- [ ] `$[0,0]`
  Input:
  ```
  [
    "a"
  ]
  ```
  Expected output:
  ```
  ["a", "a"]
  ```
  Actual output:
  ```
  [
    "a"
  ]
  ```

- [ ] `$[?(@.key<3),?(@.key>6)]`
  Input:
  ```
  [
    {
      "key": 1
    },
    {
      "key": 8
    },
    {
      "key": 3
    },
    {
      "key": 10
    },
    {
      "key": 7
    },
    {
      "key": 2
    },
    {
      "key": 6
    },
    {
      "key": 4
    }
  ]
  ```
  Error:
  ```
  path: invalid character at 12
  ```

- [ ] `$[:]['c','d']`
  Input:
  ```
  [
    {
      "c": "cc1",
      "d": "dd1",
      "e": "ee1"
    },
    {
      "c": "cc2",
      "d": "dd2",
      "e": "ee2"
    }
  ]
  ```
  Expected output:
  ```
  ["cc1", "dd1", "cc2", "dd2"]
  ```
  Actual output:
  ```
  [
    [
      "cc1",
      "dd1"
    ],
    [
      "cc2",
      "dd2"
    ]
  ]
  ```

- [ ] `$[4,1]`
  Input:
  ```
  [
    1,
    2,
    3,
    4,
    5
  ]
  ```
  Expected output:
  ```
  [5, 2]
  ```
  Actual output:
  ```
  [
    2,
    5
  ]
  ```

- [ ] `$.*[0,:5]`
  Input:
  ```
  {
    "a": [
      "string",
      null,
      true
    ],
    "b": [
      false,
      "string",
      5.4
    ]
  }
  ```
  Error:
  ```
  path: invalid character at 6
  ```

- [ ] `$[1:3,4]`
  Input:
  ```
  [
    1,
    2,
    3,
    4,
    5
  ]
  ```
  Error:
  ```
  path: invalid character at 5
  ```

- [ ] `$[*,1]`
  Input:
  ```
  [
    "first",
    "second",
    "third",
    "forth",
    "fifth"
  ]
  ```
  Expected output:
  ```
  NOT_SUPPORTED
  ```
  Actual output:
  ```
  [
    "second"
  ]
  ```


For reference, the output was generated by the program in https://github.com/cburgmer/json-path-comparison/tree/master/implementations/Golang_github.com-bhmj-jsonslice.

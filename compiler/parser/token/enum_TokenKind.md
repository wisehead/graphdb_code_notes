#1.enum TokenKind

```rust
#[derive(Logos, Clone, Copy, Debug, PartialEq, Eq, PartialOrd, Ord)]
pub enum TokenKind {
    #[error]
    Error,

    EOI,

    #[regex(r"\p{White_Space}+", logos::skip)]
    Whitespace,

    #[regex(r#"[_a-zA-Z][_$a-zA-Z0-9]*"#, priority = 3)]
    Ident,

    //#[regex(r"--[^\t\n\f]*", logos::skip)]
    #[regex(r"/\*([^\*]|(\*[^/]))*\*/", logos::skip)]
    Comment,

    #[regex(r"\p{ID_Start}\p{ID_Continue}*", priority = 2)]
    UnescapedSymbolicName,

    #[regex(r#""([^"\\]|\\.|"")*""#)]
    #[regex(r#"'([^'\\]|\\.|'')*'"#)]
    QuotedString,

    #[regex(r"0x\p{Hex_Digit}+")]
    HexInteger,

    #[regex(r"0[0-7]+")]
    OctalInteger,

    #[regex(r"0|([1-9][0-9]*)")]
    DecimalInteger,

    #[regex(r"[0-9]*\.[0-9]+")]
    RegularDecimalReal,

    #[regex(r"(([0-9]+)|([0-9]+\.[0-9]+)|(\.[0-9]+))[Ee]-?[0-9]+")]
    ExponentDecimalReal,

    // Symbols
    #[token("==")]
    DoubleEq,
    #[token("=")]
    Eq,
    #[token("<>")]
    #[token("!=")]
    NotEq,
    #[token("<")]
    Lt,
    #[token(">")]
    Gt,
    #[token("<=")]
    Le,
    #[token(">=")]
    Ge,
    #[token("+")]
    Plus,
    #[token("-")]
    Minus,
    #[token("*")]
    Multiply,
    #[token("/")]
    Divide,
    #[token("%")]
    Modulo,
    #[token("(")]
    LParen,
    #[token(")")]
    RParen,
    #[token(",")]
    Comma,
    #[token(".")]
    Period,
    #[token(":")]
    Colon,
    #[token(";")]
    SemiColon,
    #[token("[")]
    LBracket,
    #[token("]")]
    RBracket,
    #[token("|")]
    Pipe,
    #[token("..")]
    DoublePeriod,
    #[token("^")]
    Caret,
    #[token("$")]
    Dollar,
    #[token("{")]
    LBrace,
    #[token("}")]
    RBrace,

    // Keywords
    #[token("ALL", ignore(ascii_case))]
    ALL,
    #[token("ASC", ignore(ascii_case))]
    ASC,
    #[token("ASCENDING", ignore(ascii_case))]
    ASCENDING,
    #[token("BY", ignore(ascii_case))]
    BY,
    #[token("CALL", ignore(ascii_case))]
    CALL,
    #[token("CREATE", ignore(ascii_case))]
    CREATE,
    #[token("DELETE", ignore(ascii_case))]
    DELETE,
    #[token("DESC", ignore(ascii_case))]
    DESC,
    #[token("DESCENDING", ignore(ascii_case))]
    DESCENDING,
    #[token("DETACH", ignore(ascii_case))]
    DETACH,
    #[token("NODETACH", ignore(ascii_case))]
    NODETACH,
    #[token("EXISTS", ignore(ascii_case))]
    EXISTS,
    #[token("CASCADE", ignore(ascii_case))]
    CASCADE,
    #[token("LIMIT", ignore(ascii_case))]
    LIMIT,
    #[token("MATCH", ignore(ascii_case))]
    MATCH,
    #[token("MERGE", ignore(ascii_case))]
    MERGE,
    #[token("ON", ignore(ascii_case))]
    ON,
    #[token("OPTIONAL", ignore(ascii_case))]
    OPTIONAL,
    #[token("ORDER", ignore(ascii_case))]
    ORDER,
    #[token("REMOVE", ignore(ascii_case))]
    REMOVE,
    #[token("RETURN", ignore(ascii_case))]
    RETURN,
    #[token("SET", ignore(ascii_case))]
    SET,
    #[token("PASSWORD", ignore(ascii_case))]
    PASSWORD,
    #[token("INSERT", ignore(ascii_case))]
    INSERT,
    #[token("SKIP", ignore(ascii_case))]
    SKIP,
    #[token("WHERE", ignore(ascii_case))]
    WHERE,
    #[token("WITH", ignore(ascii_case))]
    WITH,
    #[token("UNION", ignore(ascii_case))]
    UNION,
    #[token("INTERSECT", ignore(ascii_case))]
    INTERSECT,
    #[token("EXCEPT", ignore(ascii_case))]
    EXCEPT,
    #[token("UNWIND", ignore(ascii_case))]
    UNWIND,
    #[token("AND", ignore(ascii_case))]
    AND,
    #[token("AS", ignore(ascii_case))]
    AS,
    #[token("CONTAINS", ignore(ascii_case))]
    CONTAINS,
    #[token("DISTINCT", ignore(ascii_case))]
    DISTINCT,
    #[token("ENDS", ignore(ascii_case))]
    ENDS,
    #[token("IN", ignore(ascii_case))]
    IN,
    #[token("IS", ignore(ascii_case))]
    IS,
    #[token("NOT", ignore(ascii_case))]
    NOT,
    #[token("OR", ignore(ascii_case))]
    OR,
    #[token("STARTS", ignore(ascii_case))]
    STARTS,
    #[token("XOR", ignore(ascii_case))]
    XOR,
    #[token("FALSE", ignore(ascii_case))]
    FALSE,
    #[token("TRUE", ignore(ascii_case))]
    TRUE,
    #[token("NULL", ignore(ascii_case))]
    NULL,
    #[token("CONSTRAINT", ignore(ascii_case))]
    CONSTRAINT,
    #[token("DO", ignore(ascii_case))]
    DO,
    #[token("FOR", ignore(ascii_case))]
    FOR,
    #[token("REQUIRE", ignore(ascii_case))]
    REQUIRE,
    #[token("UNIQUE", ignore(ascii_case))]
    UNIQUE,
    #[token("CASE", ignore(ascii_case))]
    CASE,
    #[token("WHEN", ignore(ascii_case))]
    WHEN,
    #[token("THEN", ignore(ascii_case))]
    THEN,
    #[token("ELSE", ignore(ascii_case))]
    ELSE,
    #[token("END", ignore(ascii_case))]
    END,
    #[token("MANDATORY", ignore(ascii_case))]
    MANDATORY,
    #[token("SCALAR", ignore(ascii_case))]
    SCALAR,
    #[token("OF", ignore(ascii_case))]
    OF,
    #[token("ADD", ignore(ascii_case))]
    ADD,
    #[token("DROP", ignore(ascii_case))]
    DROP,
    #[token("YIELD", ignore(ascii_case))]
    YIELD,
    #[token("EXPLAIN", ignore(ascii_case))]
    EXPLAIN,
    #[token("ALTER", ignore(ascii_case))]
    ALTER,
    #[token("CONFIG", ignore(ascii_case))]
    CONFIG,
    #[token("UNSET", ignore(ascii_case))]
    UNSET,
    #[token("RECONFIGURE", ignore(ascii_case))]
    RECONFIGURE,
    #[token("START", ignore(ascii_case))]
    START,
    #[token("COMMIT", ignore(ascii_case))]
    COMMIT,
    #[token("ROLLBACK", ignore(ascii_case))]
    ROLLBACK,
    #[token("TRANSACTION", ignore(ascii_case))]
    TRANSACTION,
    #[token("AUTOCOMMIT", ignore(ascii_case))]
    AUTOCOMMIT,
    #[token("ISOLATION", ignore(ascii_case))]
    ISOLATION,
    #[token("LEVEL", ignore(ascii_case))]
    LEVEL,
    #[token("READ COMMITTED", ignore(ascii_case))]
    READCOMMITTED,
    #[token("REPEATABLE READ", ignore(ascii_case))]
    REPEATABLEREAD,
    #[token("SHOW", ignore(ascii_case))]
    SHOW,
    #[token("GRAPHS", ignore(ascii_case))]
    GRAPHS,
    #[token("GRAPH", ignore(ascii_case))]
    GRAPH,
    #[token("USE", ignore(ascii_case))]
    USE,
    #[token("USER", ignore(ascii_case))]
    USER,
    #[token("USERS", ignore(ascii_case))]
    USERS,
    #[token("ROLE", ignore(ascii_case))]
    ROLE,
    #[token("CLEAR", ignore(ascii_case))]
    CLEAR,
    #[token("RENAME", ignore(ascii_case))]
    RENAME,
    #[token("IF", ignore(ascii_case))]
    IF,
    #[token("PARTITION_NUM", ignore(ascii_case))]
    PARTITIONNUM,
    // #[token("REPLICA_NUM", ignore(ascii_case))]
    // REPLICANUM,
    #[token("CHARSET", ignore(ascii_case))]
    CHARSET,
    #[token("COMMENT", ignore(ascii_case))]
    COMMENT,
    #[token("VERTEX", ignore(ascii_case))]
    VERTEX,
    #[token("VERTEXES", ignore(ascii_case))]
    VERTEXES,
    #[token("VERTICES", ignore(ascii_case))]
    VERTICES,
    #[token("PRIMARY", ignore(ascii_case))]
    PRIMARY,
    #[token("KEY", ignore(ascii_case))]
    KEY,
    #[token("BOOLEAN", ignore(ascii_case))]
    BOOLEAN,
    #[token("BYTE", ignore(ascii_case))]
    BYTE,
    #[token("BLOB", ignore(ascii_case))]
    BLOB,
    #[token("TEXT", ignore(ascii_case))]
    TEXT,
    #[token("UUID", ignore(ascii_case))]
    UUID,
    #[token("INT32", ignore(ascii_case))]
    #[token("INT(32)", ignore(ascii_case))]
    INT32,
    #[token("INT64", ignore(ascii_case))]
    #[token("INT(64)", ignore(ascii_case))]
    INT64,
    #[token("DOUBLE", ignore(ascii_case))]
    DOUBLE,
    #[token("FLOAT", ignore(ascii_case))]
    FLOAT,
    #[token("STRING", ignore(ascii_case))]
    STRING,
    #[token("TIMESTAMP", ignore(ascii_case))]
    TIMESTAMP,
    #[token("DEFAULT", ignore(ascii_case))]
    DEFAULT,
    #[token("RANKABLE", ignore(ascii_case))]
    RANKABLE,
    #[token("_ID", ignore(ascii_case))]
    _ID,
    #[token("_TYPE", ignore(ascii_case))]
    _TYPE,
    #[token("_FROM_ID", ignore(ascii_case))]
    _FROMID,
    #[token("_FROM_TYPE", ignore(ascii_case))]
    _FROMTYPE,
    #[token("PARTITION", ignore(ascii_case))]
    PARTITION,
    #[token("HASH", ignore(ascii_case))]
    HASH,
    #[token("UTF8", ignore(ascii_case))]
    UTF8,
    #[token("UTF8MB4", ignore(ascii_case))]
    UTF8MB4,
    #[token("GKB", ignore(ascii_case))]
    GKB,
    #[token("DDL", ignore(ascii_case))]
    DDL,
    #[token("LEADER", ignore(ascii_case))]
    LEADER,
    #[token("EDGE", ignore(ascii_case))]
    EDGE,
    #[token("EDGES", ignore(ascii_case))]
    EDGES,
    #[token("FROM", ignore(ascii_case))]
    FROM,
    #[token("TO", ignore(ascii_case))]
    TO,
    #[token("LOCKS", ignore(ascii_case))]
    LOCKS,
    #[token("COLUMN", ignore(ascii_case))]
    COLUMN,
    #[token("MODIFY", ignore(ascii_case))]
    MODIFY,
    #[token("REBUILD", ignore(ascii_case))]
    REBUILD,
    #[token("INDEX", ignore(ascii_case))]
    INDEX,
    #[token("INDEXES", ignore(ascii_case))]
    INDEXES,
    #[token("FULLTEXT", ignore(ascii_case))]
    FULLTEXT,
    #[token("STATUS", ignore(ascii_case))]
    STATUS,
    #[token("HINT", ignore(ascii_case))]
    HINT,
    #[token("COUNT", ignore(ascii_case))]
    COUNT,
    #[token("SUBMIT", ignore(ascii_case))]
    SUBMIT,
    #[token("JOB", ignore(ascii_case))]
    JOB,
    #[token("JOBS", ignore(ascii_case))]
    JOBS,
    #[token("CLEAN", ignore(ascii_case))]
    CLEAN,
    #[token("RUN", ignore(ascii_case))]
    RUN,
    #[token("CANCEL", ignore(ascii_case))]
    CANCEL,
    #[token("RESULTS", ignore(ascii_case))]
    RESULTS,
    #[token("GRANT", ignore(ascii_case))]
    GRANT,
    #[token("REVOKE", ignore(ascii_case))]
    REVOKE,
    #[token("PROPERTY", ignore(ascii_case))]
    PROPERTY,
}


```
#1.parse_statement

```
parse_statement
--map(
        rule! {
            #parse_query ~ #parse_with_hint? ~ SemiColon? ~ EOI
        },
        |(query, hints, _, _)| Statement { query, hints },
    )(input)
```

#2.map原始模板

```rust
/// Maps a function on the result of a parser.
///
/// ```rust
/// use nom::{Err,error::ErrorKind, IResult,Parser};
/// use nom::character::complete::digit1;
/// use nom::combinator::map;
/// # fn main() {
///
/// let mut parser = map(digit1, |s: &str| s.len());
///
/// // the parser will count how many characters were returned by digit1
/// assert_eq!(parser.parse("123456"), Ok(("", 6)));
///
/// // this will fail if digit1 fails
/// assert_eq!(parser.parse("abc"), Err(Err::Error(("abc", ErrorKind::Digit))));
/// # }
/// ```
pub fn map<I, O1, O2, E, F, G>(mut parser: F, mut f: G) -> impl FnMut(I) -> IResult<I, O2, E>
where
  F: Parser<I, O1, E>,
  G: FnMut(O1) -> O2,
{
  move |input: I| {
    let (input, o1) = parser.parse(input)?;
    Ok((input, f(o1)))
  }
}

```
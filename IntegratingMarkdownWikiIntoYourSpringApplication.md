Lightweight Documentation for Your Spring Web Application
=========================================================

A few weeks ago I finished reading "The Pragmatic Programmer".
This book was a kind of enlightenment for me,
but I'll come back to reviewing it extensively in a later post.
Andy Hunt and Dave Thomas present a bunch of very useful and powerful ideas.

One of the points that hit me most was the chapter "It's all Writing".
The idea is to treat any form of documentation like source code, especially

 - Keep it in your version control system (together with the source code)
 - Don't repeat yourself (Writing HTML)
 - Maintain it as thoroughly as your source code (timely!)

Recently I had the chance to implement their idea in a new project.
I wanted to make it easy for the developers to do the right thing.
The Wiki style of documentation fits these needs like a glove.
The project is based on Spring MVC.
I used a lightweight markup language for the documentation files: I chose [Markdown](links).
I integrated the Wiki right into the application itself.
I want to share my approach / implementation with you:

Implementation
--------------

The Wiki depends on the [MarkdownPapers](URL missing) library.
Since we use [Gradle](http://www.gradle.org) as our build system,
we have to add the following line to our dependency section.

    compile "org.tautua.markdownpapers:markdownpapers-core:1.2+"

Spring MVC Controller
---------------------

You need only few code in order to display MarkDown based HTML pages.
I wrote a small controller to handle requests to all URLs starting with `/wiki/`:

    @Controller
    public class WikiController {
      ResourceReaderFactory _resourceReaderFactory;

      @Autowired
      public WikiController(ResourceReaderFactory resourceReaderFactory) {
        _resourceReaderFactory = resourceReaderFactory;
      }

      @RequestMapping(value = "/wiki/{pageName}", method=RequestMethod.GET)
      public ModelAndView wikiPage(@PathVariable String pageName) throws Exception {
        String wikiFileName = String.format("/WEB-INF/wiki/%s.md", pageName);
        Reader reader = _resourceReaderFactory.createResourceReader(wikiFileName);

        return new ModelAndView("markdownView", "reader", reader);
      }
    }

I extracted a small component that provides a `Reader` for a Wiki file:

    @Component
    public class SpringResourceReaderFactory implements ResourceReaderFactory {

      @Autowired
      ApplicationContext applicationContext;

      public Reader createResourceReader(String wikiUrl) throws IOException {
        Resource resource = applicationContext.getResource(wikiUrl);
        return new InputStreamReader(resource.getInputStream());
      }
    }

(Extracting the file input from the file processing allowed me to mock the file system access.
The implementation of `ResourceReaderFactory` is based on Spring.
Since Spring provides a simple API to access classpath resources
(and Spring is known to be thoroughly tested and robust)
I did not test this implementation.
I assume it to be [too simple to break](URL IS MISSING)


MarkdownView
------------

Finally, I needed to convert the MarkDown sources to HTML.
I implemented a custom `AbstractView` to this end:

    @Component
    public class MarkdownView extends AbstractView {
      static Markdown markdown = new Markdown();

      @Override
      protected void renderMergedOutputModel(
            Map<String, Object> model,
            HttpServletRequest request,
            HttpServletResponse response) throws Exception {
        Reader reader = (Reader) model.get("reader");
        Writer writer = response.getWriter();
        markdown.transform(reader, writer);
      }
    }


A little bit of (XML) config
----------------------------

Wiring everything together is absolutely easy thanks to the
[annotation-based configuration of Spring](URL IS MISSING).
You just have to connect names based on their class names
using the `BeanNameViewResolver`:

    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
      <property name="order" value="1" />
    </bean>


Lightweight Documentation for Your Spring Web Application
=========================================================

Read The Pragmatic Programmer

Chapter: It's all Writing

Treat any form of documentation like source code
 - use version control (together with the source code)
 - Don't repeat yourself (Writing HTML)
 - Maintain it at the same standard as your source code (timely!)

Make it easy to do the right thing

lightweight markup languages: e.g. Markdown

Implementation
--------------

Dependency to MarkdownPapers

    implCompile "org.tautua.markdownpapers:markdownpapers-core:1.2+"

Controller
----------

    @Controller
    public class WikiController {
        ResourceReaderFactory _resourceReaderFactory;

        @Autowired
        public WikiController(ResourceReaderFactory resourceReaderFactory) {
            _resourceReaderFactory = resourceReaderFactory;
        }

        @RequestMapping(value = "/wiki/{pageName}", method=RequestMethod.GET)
            public ModelAndView wikiPage(@PathVariable String pageName) throws Exception {
            String wikiFileName = format("/WEB-INF/wiki/%s.md", pageName);
            Reader reader = _resourceReaderFactory.createResourceReader(wikiFileName);

            return new ModelAndView("markdownView", "reader", reader);
        }

    }

    @Component
    public class SpringResourceReaderFactory implements ResourceReaderFactory {

        @Autowired
        ApplicationContext applicationContext;

        public Reader createResourceReader(String wikiUrl) throws IOException {
            Resource resource = applicationContext.getResource(wikiUrl);
            return new InputStreamReader(resource.getInputStream());
        }

    }


MarkdownView
------------

    @Component
    public class MarkdownView extends AbstractView {
        static Markdown markdown = new Markdown();

        @Override
        protected void renderMergedOutputModel(Map<String, Object> model, HttpServletRequest request, HttpServletResponse response) throws Exception {
            Reader reader = (Reader) model.get("reader");
            Writer writer = response.getWriter();
            markdown.transform(reader, writer);
        }

    }


a little bit of (XML) config
--------------------------

    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
      <property name="order" value="1" />
    </bean>



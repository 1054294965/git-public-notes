### httpmessage:  

    父类的AbstractHttpMessageConverter方法  canWrite()判断是否支持mediatype。
    protected boolean canWrite(MediaType mediaType) {
    	if (mediaType == null || MediaType.ALL.equals(mediaType)) {
    		return true;
    	}
    	for (MediaType supportedMediaType : getSupportedMediaTypes()) {
    		if (supportedMediaType.isCompatibleWith(mediaType)) {
    			return true;
    		}
    	}
    	return false;
    }


### StringHttpMessageConverter：    

    父类AbstractHttpMessageConverter构造器设置编码和支持的mediatype类型
    public StringHttpMessageConverter(Charset defaultCharset) {
    	super(defaultCharset, MediaType.TEXT_PLAIN, MediaType.ALL);
    }

### spring源码流程：  

    dispatcherServlet类，doService(中doDispatch(request, response);)
    010:  查看是否有handlermappings 没有报错
    mappedHandler = getHandler(processedRequest);
    				if (mappedHandler == null || mappedHandler.getHandler() == null) {
    					noHandlerFound(processedRequest, response);
    					return;
    				}
    011  获取handlerAdapter
    HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());
    protected HandlerAdapter getHandlerAdapter(Object handler) throws ServletException {
    		for (HandlerAdapter ha : this.handlerAdapters) {
    			if (logger.isTraceEnabled()) {
    				logger.trace("Testing handler adapter [" + ha + "]");
    			}
    			if (ha.supports(handler)) {
    				return ha;
    			}
    		}
    		throw new ServletException("No adapter for handler [" + handler +
    				"]: The DispatcherServlet configuration needs to include a HandlerAdapter that supports this handler");
    	}

    012  拦截器preHandler
    if (!mappedHandler.applyPreHandle(processedRequest, response)) {
    					return;
    				}
    boolean applyPreHandle(HttpServletRequest request, HttpServletResponse response) throws Exception {
    		HandlerInterceptor[] interceptors = getInterceptors();
    		if (!ObjectUtils.isEmpty(interceptors)) {
    			for (int i = 0; i < interceptors.length; i++) {
    				HandlerInterceptor interceptor = interceptors[i];
    				if (!interceptor.preHandle(request, response, this.handler)) {
    					triggerAfterCompletion(request, response, null);
    					return false;
    				}
    				this.interceptorIndex = i;
    			}
    		}
    		return true;
    	}


    013  实际调用handler
    mv = ha.handle(processedRequest, response, mappedHandler.getHandler());

### registerCustomEditor可以根据field名称添加editor.  

    CustomDateEditor shipDateEditor = new CustomDateEditor(dateFormat2, true);
    binder.registerCustomEditor(Date.class, "orderDate", orderDateEditor);
    binder.registerCustomEditor(Date.class, "shipDate", shipDateEditor);

###  databinder例子：  

    Foo target = new Foo();
    DataBinder binder = new DataBinder(target);
    binder.setValidator(new FooValidator());

    // bind to the target object
    binder.bind(propertyValues);

    // validate the target object
    binder.validate();

    // get BindingResult that includes any validation errors
    BindingResult results = binder.getBindingResult();

### databinder和typeconverter：  
databinder实现了typeconverter接口和propertyEditor接口
